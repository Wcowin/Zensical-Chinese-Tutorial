---
title: Netlify 部署
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 部署指南
---

# Netlify 部署

> 使用 Netlify 部署 Zensical 网站，享受自动构建、免费 HTTPS 和全球 CDN

!!! tip "推荐使用 GitHub Pages"
    对于大多数用户，我们推荐使用 [GitHub Pages 部署](github-pages.md)，它更简单、更免费，且与 GitHub 无缝集成。

## 为什么选择 Netlify？

Netlify 是部署 Zensical 网站的最佳选择：

- ✅ **自动构建和部署** - 推送代码即自动部署
- ✅ **免费 HTTPS** - 自动配置 SSL 证书
- ✅ **全球 CDN** - 快速访问速度
- ✅ **自动预览** - 每个 PR 都有预览链接
- ✅ **自定义域名** - 支持绑定自己的域名
- ✅ **免费额度充足** - 个人项目完全够用

## 准备工作

在开始之前，确保你已经：

- [x] 安装了 Zensical
- [x] 创建了 Zensical 项目
- [x] 将项目推送到 GitHub 仓库
- [x] 注册了 [Netlify 账号](https://app.netlify.com/signup)

## 方法一：通过 Netlify 网站部署（推荐）

### 第一步：连接 GitHub 仓库

1. 登录 [Netlify](https://app.netlify.com/)
2. 点击 **Add new site** → **Import an existing project**
3. 选择 **Deploy with GitHub**
4. 授权 Netlify 访问你的 GitHub 账号
5. 选择你的 Zensical 项目仓库

### 第二步：配置构建设置

在构建设置页面，填写以下信息：

| 设置项 | 值 |
|--------|-----|
| **Branch to deploy** | `main` 或 `master` |
| **Build command** | `zensical build` |
| **Publish directory** | `site` |

!!! tip "Python 版本"
    Zensical 需要 Python 3.10+。Netlify 默认可能并非 3.10，建议在项目根目录创建 `runtime.txt` 指定版本：
    
    ```
    3.11
    ```
    
    或 `3.10`，以符合 [PyPI 要求](https://pypi.org/project/zensical/)。

### 第三步：添加构建配置文件

在项目根目录创建 `netlify.toml` 文件：

```toml
[build]
  command = "pip install zensical && zensical build"
  publish = "site"

[[redirects]]
  from = "/*"
  to = "/404.html"
  status = 404
```

!!! info "配置说明"
    - `command`: 安装 Zensical 并构建网站
    - `publish`: 指定发布目录
    - `redirects`: 配置 404 页面
    
!!! tip "Python 版本"
    要指定 Python 版本，请在项目根目录创建 `runtime.txt` 文件（而不是在 `netlify.toml` 中设置）：
    
    ```
    3.11
    ```

### 第四步：部署

1. 点击 **Deploy site** 按钮
2. 等待构建完成（通常 1-3 分钟）
3. 构建成功后，Netlify 会提供一个临时域名（如 `https://random-name-123456.netlify.app`）

## 方法二：使用 Netlify CLI 部署

### 安装 Netlify CLI

```bash
npm install -g netlify-cli
```

### 登录 Netlify

```bash
netlify login
```

### 初始化项目

在项目根目录运行：

```bash
netlify init
```

按照提示选择：

1. **Create & configure a new site** - 创建新站点
2. 选择你的团队
3. 输入站点名称（可选）
4. **Build command**: `zensical build`
5. **Publish directory**: `site`

### 部署网站

```bash
# 构建并部署
zensical build
netlify deploy --prod
```

## 配置自定义域名

### 第一步：在 Netlify 添加域名

1. 进入你的站点设置
2. 点击 **Domain management** → **Add custom domain**
3. 输入你的域名（如 `example.com`）
4. 点击 **Verify**

### 第二步：配置 DNS

在你的域名注册商处，添加以下 DNS 记录：

#### 使用 Netlify DNS（推荐）

Netlify 会提供 4 个 Name Server，在域名注册商处修改 NS 记录：

```
dns1.p01.nsone.net
dns2.p01.nsone.net
dns3.p01.nsone.net
dns4.p01.nsone.net
```

#### 使用 CNAME 记录

如果不想更换 DNS，可以添加 CNAME 记录：

| 类型 | 名称 | 值 |
|------|------|-----|
| CNAME | www | your-site.netlify.app |
| A | @ | 75.2.60.5 |

!!! warning "DNS 生效时间"
    DNS 记录修改后，可能需要 24-48 小时才能完全生效。

### 第三步：启用 HTTPS

1. 等待 DNS 生效
2. Netlify 会自动配置 Let's Encrypt SSL 证书
3. 启用 **Force HTTPS** 选项

## 环境变量配置

如果你的项目需要环境变量（如 API 密钥），可以在 Netlify 中配置：

1. 进入站点设置
2. 点击 **Build & deploy** → **Environment**
3. 点击 **Add variable**
4. 添加你的环境变量

示例：

```
GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX
```

## 自动部署配置

### 启用自动部署

Netlify 默认启用自动部署。每次推送到主分支时，会自动触发构建。

### 部署预览

对于 Pull Request，Netlify 会自动创建预览部署：

1. 创建 PR
2. Netlify 自动构建预览版本
3. 在 PR 中查看预览链接
4. 合并 PR 后自动部署到生产环境

### 部署通知

配置部署通知：

1. 进入站点设置
2. 点击 **Build & deploy** → **Deploy notifications**
3. 添加通知（Email、Slack、Webhook 等）

## 性能优化

### 启用资源优化

在 Netlify 设置中启用：

1. **Asset optimization**
   - Bundle CSS
   - Minify CSS
   - Minify JS
   - Compress images

2. **Post processing**
   - Pretty URLs
   - Prerendering

### 配置缓存

在 `netlify.toml` 中配置缓存：

```toml
[[headers]]
  for = "/*"
  [headers.values]
    Cache-Control = "public, max-age=0, must-revalidate"

[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "/*.css"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "/*.js"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

## 常见问题

### 构建失败

**问题**：构建时提示 `zensical: command not found`

**解决方案**：确保 `netlify.toml` 中的构建命令包含安装步骤：

```toml
[build]
  command = "pip install zensical && zensical build"
```

### Python 版本问题

**问题**：需要特定的 Python 版本

**解决方案**：在 `runtime.txt` 中指定版本：

```
3.11
```

### 404 页面不生效

**问题**：自定义 404 页面不显示

**解决方案**：在 `netlify.toml` 中添加重定向规则：

```toml
[[redirects]]
  from = "/*"
  to = "/404.html"
  status = 404
```

### 部署时间过长

**问题**：每次部署需要很长时间

**解决方案**：

1. 使用依赖缓存
2. 优化构建命令
3. 减少不必要的依赖

## 完整配置示例

### netlify.toml

```toml
[build]
  command = "pip install zensical && zensical build"
  publish = "site"

# 404 页面
[[redirects]]
  from = "/*"
  to = "/404.html"
  status = 404

# 缓存配置
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"

[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

### runtime.txt

```
3.11
```

### requirements.txt

```
zensical
```

## 下一步

- 查看 [Netlify 文档](https://docs.netlify.com/)

---

**参考资料**：  

- [Netlify 官方文档](https://docs.netlify.com/)  
- [Zensical 官方文档](https://zensical.org/docs/)
