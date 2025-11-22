---
title: GitLab Pages 部署
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 部署指南
---

# GitLab Pages 部署

> 使用 GitLab Pages 免费托管你的 Zensical 网站

## 什么是 GitLab Pages？

GitLab Pages 是 GitLab 提供的免费静态网站托管服务：

- ✅ **完全免费** - 无需任何费用
- ✅ **自动 HTTPS** - 免费 SSL 证书
- ✅ **自定义域名** - 支持绑定域名
- ✅ **GitLab 集成** - 与仓库无缝集成
- ✅ **CI/CD 集成** - 使用 GitLab CI 自动部署

## 准备工作

在开始之前，确保你已经：

- [x] 拥有 GitLab 账号
- [x] 创建了 Zensical 项目
- [x] 将项目推送到 GitLab 仓库

## 配置 GitLab CI

### 第一步：修改输出目录

在 `zensical.toml` 中，将 `site_dir` 设置为 `public`（GitLab Pages 要求）：

```toml
[project]
site_dir = "public"
```

### 第二步：创建 GitLab CI 配置

在项目根目录创建 `.gitlab-ci.yml` 文件：

```yaml
pages:
  stage: deploy
  image: python:latest
  script:
    - pip install zensical
    - zensical build --clean # (1)!
  artifacts:
    paths:
      - public
  rules:
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
```

!!! note "关于缓存"
    目前，我们不推荐在 CI 系统中使用缓存，因为缓存功能将在我们优化 Zensical 性能时进行修订。

### 第三步：推送代码触发部署

```bash
git add .
git commit -m "Add GitLab CI configuration"
git push origin main
```

GitLab CI 会自动构建并部署你的网站。

### 第四步：访问网站

部署成功后，你的网站将在以下地址可用：

```
https://<username>.gitlab.io/<repository>/
```

例如：`https://username.gitlab.io/my-zensical-site/`

## 配置自定义域名

### 第一步：在 GitLab 添加域名

1. 进入项目设置
2. 点击 **Pages** → **New domain**
3. 输入你的域名（如 `example.com`）
4. 点击 **Create new domain**

### 第二步：配置 DNS

在你的域名注册商处，添加以下 DNS 记录：

#### 使用 CNAME 记录（推荐）

| 类型 | 名称 | 值 |
|------|------|-----|
| CNAME | www | `<username>.gitlab.io` |

#### 使用 A 记录

| 类型 | 名称 | 值 |
|------|------|-----|
| A | @ | 35.185.44.232 |

!!! warning "DNS 生效时间"
    DNS 记录修改后，可能需要 24-48 小时才能完全生效。

### 第三步：验证域名

1. 等待 DNS 生效
2. 在 GitLab Pages 设置中点击 **Verify**
3. 验证成功后，启用 **Force HTTPS**

## 高级配置

### 指定 Python 版本

如果需要特定版本的 Python，可以修改镜像：

```yaml
pages:
  stage: deploy
  image: python:3.11
  script:
    - pip install zensical
    - zensical build --clean
  artifacts:
    paths:
      - public
  rules:
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
```

### 使用缓存（不推荐）

虽然不推荐，但如果需要，可以这样配置：

```yaml
pages:
  stage: deploy
  image: python:latest
  cache:
    paths:
      - .cache/pip
  script:
    - pip install zensical
    - zensical build --clean
  artifacts:
    paths:
      - public
  rules:
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
```

!!! warning "缓存警告"
    目前不推荐使用缓存，因为缓存功能将在优化 Zensical 性能时进行修订。

### 多分支部署

如果需要部署多个分支，可以修改规则：

```yaml
pages:
  stage: deploy
  image: python:latest
  script:
    - pip install zensical
    - zensical build --clean
  artifacts:
    paths:
      - public
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
    - if: '$CI_COMMIT_BRANCH == "develop"'
```

## 配置 site_url

如果你的网站部署在子路径（如 `https://username.gitlab.io/repository/`），需要在 `zensical.toml` 中配置：

```toml
[project]
site_url = "https://username.gitlab.io/repository/"
site_dir = "public"
```

这样可以确保：

- ✅ 链接正确生成
- ✅ 资源路径正确
- ✅ 即时导航正常工作

## 常见问题

### 404 错误

**问题**：访问网站时出现 404 错误

**解决方案**：

1. 检查 `site_url` 配置是否正确
2. 确保 `site_dir` 设置为 `public`
3. 检查 GitLab CI 配置是否正确
4. 等待几分钟让部署生效

### 样式丢失

**问题**：网站样式不正常

**解决方案**：

1. 确保 `site_url` 配置正确
2. 检查 `use_directory_urls` 设置
3. 查看 GitLab CI 构建日志

### 自定义域名不生效

**问题**：自定义域名无法访问

**解决方案**：

1. 检查 DNS 记录是否正确
2. 等待 DNS 生效（最多 48 小时）
3. 在 GitLab 中验证域名
4. 确保已启用 HTTPS

### 构建失败

**问题**：GitLab CI 构建失败

**解决方案**：

1. 查看 CI/CD 日志
2. 检查 Python 版本是否正确
3. 确保所有依赖都已安装
4. 检查 `zensical.toml` 语法

## 完整配置示例

### .gitlab-ci.yml

```yaml
pages:
  stage: deploy
  image: python:latest
  script:
    - pip install zensical
    - zensical build --clean
  artifacts:
    paths:
      - public
  rules:
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
```

### zensical.toml

```toml
[project]
name = "My Zensical Site"
site_url = "https://username.gitlab.io/repository/"
site_dir = "public"
```

## 与 GitHub Pages 对比

| 特性 | GitLab Pages | GitHub Pages |
|------|-------------|--------------|
| **价格** | 免费 | 免费 |
| **自动部署** | ✅ GitLab CI | ✅ GitHub Actions |
| **自定义域名** | ✅ 支持 | ✅ 支持 |
| **HTTPS** | ✅ 免费 | ✅ 免费 |
| **构建时间** | 较快 | 较慢 |
| **私有仓库** | ✅ 支持 | ❌ 仅公开仓库 |
| **CI/CD** | ✅ 内置 | ✅ 需要配置 |

## 下一步

- 查看 [GitLab Pages 文档](https://docs.gitlab.com/ee/user/project/pages/)
- 考虑使用 [Netlify 部署](netlify.md)（更强大）

---

**参考资料**：
- [GitLab Pages 官方文档](https://docs.gitlab.com/ee/user/project/pages/)  
- [GitLab CI/CD 文档](https://docs.gitlab.com/ee/ci/)  
- [Zensical 官方文档](https://zensical.org/docs/)

