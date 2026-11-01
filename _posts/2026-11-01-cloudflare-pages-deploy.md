---
title: "这个博客是怎么挂到 Cloudflare Pages 上的"
date: 2026-11-01 21:00:00 +0800
categories: [博客, 记录]
tags: [Cloudflare, Pages, Jekyll, DNS, 部署]
author: adnini983
media_subpath: /assets/img/posts/cloudflare-pages-deploy/
toc: true
pin: false
---

> **声明**：本文为事后回忆整理，并非部署时实时记录，细节可能有所出入；撰写过程中有 AI 辅助。
{: .prompt-info }

现在这个站点有两条独立的访问链路：

| 入口 | 提供方 | 构建方式 |
|---|---|---|
| `adnini983.com` | **Cloudflare Pages** | Cloudflare 直接从 GitHub 仓库构建 |
| `adnini983.github.io` | GitHub Pages | GitHub Actions 构建后发布 |

本文记录主域那条链路是怎么搭起来的。全程使用 Cloudflare 的**免费套餐**，没有任何付费服务。

## 为什么还要多这一层

GitHub Pages 本身没什么问题，但多一条链路有几个实际好处：

- **构建与托管分离**：Cloudflare 从仓库独立构建，GitHub 那边挂了这边还在。
- **自带全球 CDN**：静态资源就近分发，国内访问通常也比 `github.io` 稳定些。
- **免费 SSL**：绑定自定义域后自动签发证书，不需要自己折腾。
- **可以绑根域**：想要 `example.com` 而不是 `example.github.io`，这一步绕不开。
- **免费套餐够用**：个人博客的构建次数与流量远达不到上限。

代价是：**同一份内容会被构建两次**，两边行为可能出现细微差异，这个后面「踩过的坑」会细说。

## 一、把根域接入 Cloudflare

顺序很重要：**先在 Cloudflare 添加站点，再去改 NS**。因为那对 NS 地址是 Cloudflare 在你添加站点时才分配的，先改 NS 会没有地址可填。

1. 注册 Cloudflare 账号，在添加站点时选择 **Free** 套餐。
2. 填写根域（例如 `adnini983.com`），不要带 `www` 或 `https://`。
3. Cloudflare 会扫描该域名现有的 DNS 记录，并分配一对专属的 NS，形如：

   ```
   aria.ns.cloudflare.com
   uriah.ns.cloudflare.com
   ```

   这两条是**每个账号不同**的，不要照抄别人的。

4. 登录域名提供商的管理后台，把域名的 NS 记录改成上面这两条，**删掉原有的 NS**。
5. 等待。Cloudflare 检测到 NS 变更后会自动接管，通常几分钟到几小时；控制台显示「有效」即可。

> 这一步只是让 Cloudflare 成为你域名的权威 DNS，还没有开始建站。

## 二、清理 DNS 记录

Cloudflare 接管后，在 **DNS → 记录** 里只看得到扫描到的旧记录。这时候先把不需要的清掉，只保留真正在用的，避免后面和 Pages 自动生成的记录打架。

我这个域名只保留了邮件相关的三条（内容从略）：

| 类型 | 名称 | 代理状态 | 说明 |
|---|---|---|---|
| `MX` | 根域 | **仅 DNS** | 邮件服务器 |
| `TXT` | 根域 | **仅 DNS** | SPF |
| `TXT` | `<选择器>._domainkey` | **仅 DNS** | DKIM 公钥 |

![Cloudflare 的 DNS 记录列表，只保留邮件相关条目，其余删除](dns-records.png)

⚠️ **邮件相关记录必须是「仅 DNS」（灰云），不能开代理（橙云）**。MX 记录本来就不支持代理，TXT 开了代理也会让验证失效。

其余的记录——尤其是 A / AAAA / CNAME——如果暂时用不上，一并删掉。站点本身的记录稍后由 Pages 绑定自定义域时自动创建。

## 三、让 Cloudflare Pages 接上 GitHub 仓库

1. 进入 **Workers 和 Pages → 创建 → Pages → 连接到 Git**。
2. 授权 Cloudflare 访问 GitHub，选择这个博客仓库。
3. 选择分支（本仓库是 `master`）。
4. 填写构建配置：

   | 项 | 值 |
   |---|---|
   | 框架预设 | `Jekyll`（没有就选 `None`，下面手动填） |
   | 构建命令 | `bundle exec jekyll build` |
   | 构建输出目录 | `_site` |

5. 保存并部署，等待第一次构建完成，会给一个 `xxx.pages.dev` 的临时域名。

构建失败时，Pages 的构建日志里有完整的 bundler / Jekyll 输出，比 GitHub Actions 的日志还直白，排查很方便。

## 四、构建环境变量

第一次构建大概率会遇到编码问题或依赖装不全。在项目的 **设置 → 变量和密钥** 里补几条普通变量即可：

| 变量名 | 值 | 作用 |
|---|---|---|
| `RUBY_VERSION` | `3.4.4` | 指定构建用的 Ruby 版本，与本地保持一致 |
| `LANG` | `C.UTF-8` | 避免中文内容在构建时出现编码错误 |
| `LC_ALL` | `C.UTF-8` | 同上，覆盖全部本地化类别 |
| `BUNDLE_WITHOUT` | `development test` | 跳过开发与测试依赖，缩短构建时间 |

![Cloudflare Pages 的「变量和密钥」配置界面](env-vars.png)

几点说明：

- 变量名必须准确写作 **`BUNDLE_WITHOUT`**。这类环境变量拼错时不会报错，只会被静默忽略，等到发现构建变慢再往回查就很费劲了。
- `LANG` 和 `LC_ALL` 都设 `C.UTF-8` 而不是 `zh_CN.UTF-8`，是因为精简构建镜像里不一定装了中文 locale，而 `C.UTF-8` 一定可用，对 UTF-8 内容足够。
- `BUNDLE_WITHOUT` 用空格分隔多个分组，不是逗号。

## 五、绑定自定义域

构建成功、`pages.dev` 能打开之后：

1. Pages 项目 → **自定义域** → **设置自定义域**。
2. 依次添加**根域**和 `www` 子域：

   ```
   adnini983.com
   www.adnini983.com
   ```

3. Cloudflare 会自动在 DNS 里创建对应的记录（根域是扁平的 A/AAAA，`www` 通常是 CNAME），并签发证书。**这些记录不要手动去改**。
4. 再等。证书签发和 DNS 生效官方说明最长可能到 **48 小时**，实际通常几分钟。

绑定成功后，两个域名都会出现在项目概览上，和 `pages.dev` 并列。

## 六、验证

```bash
# 证书与响应头
curl -I https://example.com

# 站点是否正常
curl -s https://example.com/robots.txt
```

如果 `www` 打不开而根域正常，通常是 `www` 的那条记录没建好，回「自定义域」页面看该域名的状态即可。

## 七、踩过的坑

### 1. 浅克隆导致「更新于」全部丢失

本站用 `_posts-lastmod-hook.rb` 读取 git 提交时间，来显示文章的「最近更新」和「更新于」。这个钩子依赖 `git rev-list --count` 判断文件被改过几次。

但 **Cloudflare Pages 的构建是浅克隆**，历史里只有一个提交，计数恒为 1，钩子判断「没改过」，于是所有文章都拿不到修改时间。结果就是：同一篇文章，在主域上不显示「更新于」，在 `github.io` 上正常显示。

修法是在构建命令前补一句：

```bash
git fetch --unshallow || true; bundle install && bundle exec jekyll build
```

### 2. GitHub Pages 的旧版构建器会抢发布

这条和 Cloudflare 无关，但非常容易混淆。如果 GitHub 仓库的 Pages 仍配置为「分支部署」，那么每次 push 会同时触发**两个**发布者：你自己的 Actions 工作流，以及 GitHub 自带的 `pages-build-deployment`。

根目录有 `.nojekyll` 时，后者会**跳过 Jekyll、把仓库原文直接发布**。于是站点会短暂变成未渲染的源文件——首页显示 `--- layout: home ---` 这样的 front matter。

根治办法是在仓库 **Settings → Pages → Source** 选择 **GitHub Actions**，让旧版构建器彻底消失。

### 3. 记录开了代理导致邮件验证失败

MX、SPF、DKIM 这类记录必须保持「仅 DNS」。如果为了让流量走 Cloudflare 而全开橙云，邮件会直接失效，而且不容易第一时间发现。

## 八、检查清单

- [ ] Cloudflare 免费套餐已添加根域
- [ ] 域名提供商的 NS 已改为 Cloudflare 分配的两条
- [ ] DNS 记录只保留邮件等必要条目，且邮件记录均为「仅 DNS」
- [ ] Pages 已连接 GitHub 仓库与正确分支
- [ ] 构建命令 `bundle exec jekyll build`、输出目录 `_site`
- [ ] 环境变量 `RUBY_VERSION` / `LANG` / `LC_ALL` / `BUNDLE_WITHOUT` 拼写正确
- [ ] 根域与 `www` 已加入「自定义域」
- [ ] 两个域名都能打开、证书正常
- [ ] 站点的 canonical / sitemap 已指向主域

---

把这一套走完，博客就有了一个不依赖 GitHub Pages 的正式入口。剩下要操心的只有一件事：**内容**。
