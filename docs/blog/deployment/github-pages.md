---
title: GitHub Pages 部署
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 部署指南
---

# GitHub Pages 部署

> 使用 GitHub Pages 免费托管你的 Zensical 网站

## 什么是 GitHub Pages？

GitHub Pages 是 GitHub 提供的免费静态网站托管服务：

- ✅ **完全免费** - 无需任何费用
- ✅ **自动 HTTPS** - 免费 SSL 证书
- ✅ **自定义域名** - 支持绑定域名
- ✅ **GitHub 集成** - 与仓库无缝集成
- ✅ **简单易用** - 推送即部署

## 准备工作

在开始之前，确保你已经：

- [x] 拥有 GitHub 账号
- [x] 创建了 Zensical 项目
- [x] 将项目推送到 GitHub 仓库

## 方法一：使用 GitHub Actions 自动部署（推荐）

### 第一步：创建 GitHub Actions 工作流

在项目根目录创建 `.github/workflows/docs.yml` 文件：

```yaml
name: Deploy Zensical to GitHub Pages

on:
  push:
    branches:
      - main  # 或 master
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # 获取完整历史，用于 git-revision-date-localized 插件

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'

      - name: Install dependencies
        run: |
          pip install zensical

      - name: Build site
        run: |
          zensical build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 第二步：配置 GitHub Pages

1. 进入 GitHub 仓库
2. 点击 **Settings** → **Pages**
3. 在 **Source** 下选择 **GitHub Actions**
4. 保存设置

### 第三步：推送代码触发部署

```bash
git add .
git commit -m "Add GitHub Actions workflow"
git push origin main
```

GitHub Actions 会自动构建并部署你的网站。

### 第四步：访问网站

部署成功后，你的网站将在以下地址可用：

```
https://<username>.github.io/<repository>/
```

例如：`https://wcowin.github.io/Zensical-Chinese-Tutorial/`

## 方法二：手动部署

### 第一步：构建网站

在本地构建网站：

```bash
zensical build
```

### 第二步：创建 gh-pages 分支

```bash
# 创建并切换到 gh-pages 分支
git checkout --orphan gh-pages

# 删除所有文件
git rm -rf .

# 复制构建文件
cp -r site/* .

# 添加 .nojekyll 文件（禁用 Jekyll）
touch .nojekyll

# 提交
git add .
git commit -m "Deploy to GitHub Pages"

# 推送
git push origin gh-pages
```

### 第三步：配置 GitHub Pages

1. 进入 GitHub 仓库设置
2. 点击 **Settings** → **Pages**
3. 在 **Source** 下选择 **Deploy from a branch**
4. 选择 **gh-pages** 分支和 **/ (root)** 目录
5. 点击 **Save**

## 配置自定义域名

### 第一步：添加 CNAME 文件

在 `docs/` 目录下创建 `CNAME` 文件：

```
example.com
```

或者在 `zensical.toml` 中配置：

```toml
[project]
site_url = "https://example.com"
```

### 第二步：配置 DNS

在域名注册商处添加以下 DNS 记录：

#### 使用 A 记录（推荐）

| 类型 | 名称 | 值 |
|------|------|-----|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

#### 使用 CNAME 记录

| 类型 | 名称 | 值 |
|------|------|-----|
| CNAME | www | <username>.github.io |

### 第三步：在 GitHub 设置自定义域名

1. 进入 **Settings** → **Pages**
2. 在 **Custom domain** 输入你的域名
3. 点击 **Save**
4. 等待 DNS 检查通过
5. 勾选 **Enforce HTTPS**

!!! warning "DNS 生效时间"
    DNS 记录修改后，可能需要 24-48 小时才能完全生效。

## 配置 site_url

如果你的网站部署在子路径（如 `https://username.github.io/repository/`），需要在 `zensical.toml` 中配置：

```toml
[project]
site_url = "https://username.github.io/repository/"
```

这样可以确保：

- ✅ 链接正确生成
- ✅ 资源路径正确
- ✅ 即时导航正常工作

## 优化部署速度

### 使用缓存

在 GitHub Actions 中启用缓存：

```yaml
- name: Setup Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.11'
    cache: 'pip'  # 启用 pip 缓存
```

### 并行构建

如果项目较大，可以考虑并行构建：

```yaml
- name: Build site
  run: |
    zensical build --parallel
```

### 增量构建

对于大型项目，可以使用增量构建：

```yaml
- name: Build site
  run: |
    zensical build --dirty
```

## 常见问题

### 404 错误

**问题**：访问网站时出现 404 错误

**解决方案**：

1. 检查 `site_url` 配置是否正确
2. 确保 GitHub Pages 已启用
3. 检查分支和目录设置是否正确
4. 等待几分钟让部署生效

### 样式丢失

**问题**：网站样式不正常

**解决方案**：

1. 确保 `site_url` 配置正确
2. 检查 `use_directory_urls` 设置
3. 添加 `.nojekyll` 文件禁用 Jekyll

### 自定义域名不生效

**问题**：自定义域名无法访问

**解决方案**：

1. 检查 DNS 记录是否正确
2. 等待 DNS 生效（最多 48 小时）
3. 确保 CNAME 文件存在
4. 在 GitHub 设置中重新保存域名

### 构建失败

**问题**：GitHub Actions 构建失败

**解决方案**：

1. 查看 Actions 日志
2. 检查 Python 版本是否正确
3. 确保所有依赖都已安装
4. 检查 `zensical.toml` 语法

## 完整配置示例

### .github/workflows/docs.yml

```yaml
name: Deploy Zensical

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'

      - name: Install Zensical
        run: pip install zensical

      - name: Build
        run: zensical build

      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

### CNAME

```
example.com
```

### .nojekyll

创建空文件即可（禁用 Jekyll 处理）。

## 与 Netlify 对比

| 特性 | GitHub Pages | Netlify |
|------|-------------|---------|
| **价格** | 免费 | 免费（有限额） |
| **自动部署** | ✅ GitHub Actions | ✅ 自动 |
| **自定义域名** | ✅ 支持 | ✅ 支持 |
| **HTTPS** | ✅ 免费 | ✅ 免费 |
| **构建时间** | 较慢 | 较快 |
| **CDN** | GitHub CDN | 全球 CDN |
| **预览部署** | ❌ 需配置 | ✅ 自动 |
| **环境变量** | ❌ 不支持 | ✅ 支持 |

## 下一步

- 配置 [自定义域名](#配置自定义域名)
- 优化 [部署速度](#优化部署速度)
- 查看 [GitHub Pages 文档](https://docs.github.com/pages)
- 考虑使用 [Netlify 部署](netlify.md)（更强大）

---

**参考资料**：
- [GitHub Pages 官方文档](https://docs.github.com/pages)
- [GitHub Actions 文档](https://docs.github.com/actions)
- [Zensical 官方文档](https://zensical.org/docs/)
