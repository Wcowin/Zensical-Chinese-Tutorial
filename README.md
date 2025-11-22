# Zensical-Wcowin 中文教程

> 🚀 **MkDocs 已停止更新，Zensical 是官方推荐的新一代静态网站生成器**

- **现代化设计，性能优异**  
- **即时导航，流畅体验**  
- **博客系统，开箱即用**  
- **中文教程，详细完整**  
- **简单易上手，小白友好**  
- **𝕙𝕒𝕧𝕖 𝕒 𝕘𝕠𝕠𝕕 𝕥𝕚𝕞𝕖 !**

## 目录
- [Zensical-Wcowin 中文教程](#zensical-wcowin-中文教程)
  - [目录](#目录)
  - [为什么选择 Zensical](#为什么选择-zensical)
  - [快速开始](#快速开始)
    - [环境要求](#环境要求)
    - [方法一：直接下载使用（推荐新手）](#方法一直接下载使用推荐新手)
    - [方法二：Git克隆使用](#方法二git克隆使用)
    - [方法三：GitHub模板创建](#方法三github模板创建)
  - [核心概念](#核心概念)
    - [项目结构](#项目结构)
    - [配置文件详解](#配置文件详解)
    - [博客系统](#博客系统)
  - [常见问题解决](#常见问题解决)
      - [🔧 依赖安装问题](#-依赖安装问题)
      - [🔧 Python版本问题](#-python版本问题)
      - [🔧 端口占用问题](#-端口占用问题)
    - [自定义配置](#自定义配置)
    - [🚀 部署到线上](#-部署到线上)
  - [高级功能](#高级功能)
    - [即时导航](#即时导航)
    - [搜索功能](#搜索功能)
    - [多语言支持](#多语言支持)
- [联系方式](#联系方式)
  - [案例成果](#案例成果)
  - [贡献者](#贡献者)
  - [License](#license)

## 为什么选择 Zensical

| 特性 | Zensical | MkDocs |
|------|----------|--------|
| **维护状态** | ✅ 积极开发 | ⚠️ 已停止更新 |
| **即时导航** | ✅ 原生支持 | ❌ 需要插件 |
| **博客系统** | ✅ 开箱即用 | ⚠️ 需要插件 |
| **性能** | ✅ 优异 | ⚠️ 一般 |
| **现代化** | ✅ 现代设计 | ⚠️ 传统设计 |
| **中文支持** | ✅ 完整 | ✅ 完整 |

**Zensical 的核心优势：**
- 🚀 **即时导航** - 无需刷新页面，流畅切换内容
- 📝 **博客系统** - 内置博客插件，支持标签、分类、日期等
- ⚡ **高性能** - 优化的渲染引擎，快速加载
- 🎨 **现代设计** - 遵循最新的 Web 设计规范
- 🔧 **易于定制** - 灵活的配置系统，支持自定义样式

## 快速开始

### 环境要求

在开始之前，请确保你的系统已安装：

- **Python 3.8+** （推荐3.9或更高版本）
- **pip** （Python包管理器）
- **Git** （用于版本控制）

### 方法一：直接下载使用（推荐新手）

这是最简单的方式，适合初学者快速体验：

1. **下载模板**
   - 访问 [Releases页面](https://github.com/Wcowin/Zensical-Chinese-Tutorial/releases)
   - 下载最新版本的 `Zensical-Wcowin.zip`
   - 解压到你想要的目录
   - 比如你在本地新建了一个 `myblog` 文件夹，就把所有文件移动到该目录

2. **安装依赖**
   ```bash
   # 建议在虚拟环境中安装
   pip install -r requirements.txt
   ```

3. **启动预览**
   ```bash
   # 进入项目目录
   cd myblog
   
   # 启动本地服务器
   zensical serve
   ```

4. **查看效果**
   - 打开浏览器访问 `http://127.0.0.1:8000`
   - 实时预览你的网站

### 方法二：Git克隆使用

适合有Git基础的用户：

1. **克隆仓库**
   ```bash
   # 克隆到本地
   git clone https://github.com/Wcowin/Zensical-Chinese-Tutorial.git
   
   # 进入项目目录
   cd Zensical-Wcowin
   ```

2. **安装依赖**
   ```bash
   # 安装所有必需的包
   pip install -r requirements.txt
   ```

3. **启动服务**
   ```bash
   # 启动开发服务器
   zensical serve
   ```

### 方法三：GitHub模板创建

最适合想要部署到GitHub Pages的用户：

1. **使用模板创建仓库**
   - 点击 [使用此模板](https://github.com/new?template_name=Zensical-Wcowin&template_owner=Wcowin)
   - 创建你自己的仓库（建议命名为 `你的用户名.github.io`）

2. **克隆到本地**
   ```bash
   git clone https://github.com/你的用户名/你的仓库名.git
   cd 你的仓库名
   ```

3. **配置和部署**
   ```bash
   # 安装依赖
   pip install -r requirements.txt
   
   # 本地预览
   zensical serve
   
   # 部署到 Netlify（推荐）
   # 或部署到 GitHub Pages
   ```

## 核心概念

### 项目结构

```
.
├── .github/                    # GitHub 配置
├── docs/                       # 文档源文件
│   ├── index.md               # 首页
│   ├── blog/                  # 博客文章
│   │   ├── posts/            # 博客文章目录
│   │   └── index.md          # 博客首页
│   ├── stylesheets/          # 自定义样式
│   │   └── extra.css         # 额外样式
│   ├── javascripts/          # 自定义脚本
│   │   └── extra.js          # 额外脚本
│   └── assets/               # 静态资源
├── overrides/                 # 模板覆盖
│   ├── partials/             # 部分模板
│   ├── 404.html              # 自定义 404 页面
│   └── footer.html           # 自定义页脚
├── zensical.toml             # Zensical 配置文件
├── requirements.txt          # Python 依赖
└── site/                     # 构建输出目录
```

### 配置文件详解

**zensical.toml** 是 Zensical 的核心配置文件：

```toml
[project]
# 基本信息
site_name = "我的博客"
site_url = "https://example.com"
site_author = "你的名字"

# 主题配置
[project.theme]
variant = "modern"              # 使用 modern 主题
custom_dir = "overrides"        # 自定义模板目录
language = "zh"                 # 语言设置

# 博客插件
[project.plugins.blog]
post_date_format = "full"       # 日期格式
draft = true                    # 启用草稿功能
post_readtime = true            # 显示阅读时间

# Markdown 扩展
[project.markdown_extensions]
abbr = {}
attr_list = {}
# ... 更多扩展
```

### 博客系统

Zensical 的博客系统功能强大：

1. **创建博客文章**
   ```markdown
   ---
   date: 2025-01-22
   authors:
     - name: 你的名字
       email: your@email.com
   categories:
     - 技术
     - Python
   ---
   
   # 文章标题
   
   文章内容...
   ```

2. **支持的功能**
   - ✅ 自动生成博客索引
   - ✅ 按日期、分类、标签筛选
   - ✅ 自动计算阅读时间
   - ✅ 作者信息展示
   - ✅ 文章摘要生成

3. **草稿管理**
   ```markdown
   ---
   draft: true
   ---
   ```
   标记为草稿的文章在生产环境中不会显示

## 常见问题解决

#### 🔧 依赖安装问题

如果遇到依赖缺失错误：

```bash
# 单独安装缺失的包
pip install zensical

# 或者一次性安装所有依赖
pip install -r requirements.txt
```

#### 🔧 Python版本问题

如果提示Python版本过低：

```bash
# 检查Python版本
python --version

# 如果版本低于3.8，请升级Python
# 或使用虚拟环境
python -m venv zensical-env
source zensical-env/bin/activate  # Linux/Mac
# 或
zensical-env\Scripts\activate     # Windows
```

#### 🔧 端口占用问题

如果8000端口被占用：

```bash
# 使用其他端口
zensical serve -a 127.0.0.1:8080
```

###  自定义配置

1. **修改网站信息**
   - 编辑 `zensical.toml` 文件
   - 修改 `site_name`、`site_author` 等基本信息

2. **添加博客文章**
   - 在 `docs/blog/posts/` 目录下创建 Markdown 文件
   - 添加 front matter 元数据（日期、作者、分类等）

3. **个性化样式**
   - 修改 `docs/stylesheets/extra.css`
   - 自定义颜色、字体等样式
   - 在 `zensical.toml` 中配置 `extra_css`

4. **自定义模板**
   - 在 `overrides/` 目录下创建模板文件
   - 覆盖默认的主题模板

### 🚀 部署到线上

**Netlify 部署（推荐）：**
```bash
# 1. 构建静态文件
zensical build

# 2. 连接 GitHub 仓库到 Netlify
# 3. 配置构建命令：zensical build
# 4. 配置发布目录：site
```

**GitHub Pages 部署：**
```bash
# 1. 构建静态文件
zensical build

# 2. 提交到 GitHub
git add .
git commit -m "Deploy site"
git push origin main

# 3. 在 GitHub 仓库设置中启用 Pages
# 4. 选择 GitHub Actions 作为部署方式
```

**自托管部署：**
```bash
# 构建静态文件
zensical build

# 将 site/ 目录上传到你的服务器
# 配置 Web 服务器（Nginx/Apache）指向 site/ 目录
```

---

**💡 提示：** 更多详细信息请查看 [Zensical 官方文档](https://zensical.org/docs/)

## 高级功能

### 即时导航

Zensical 内置即时导航功能，无需刷新页面即可切换内容：

```toml
[project.extra]
instant_loading = true  # 启用即时加载
instant_prefetch = true # 启用预加载
```

### 搜索功能

配置全文搜索：

```toml
[project.plugins.search]
separator = '[\s\u200b\-]'  # 搜索分隔符
```

### 多语言支持

```toml
[project]
language = "zh"  # 中文

[[project.extra.alternate]]
name = "English"
link = "javascript:translateTo('english');"
lang = "en"
```

# 联系方式

<center>

**微信**  
<a href="https://pic3.zhimg.com/80/v2-5ef3dde831c9d0a41fe35fabb0cb8784_1440w.webp" target="_blank">
<img src="https://pic3.zhimg.com/80/v2-5ef3dde831c9d0a41fe35fabb0cb8784_1440w.webp" style="width: 450px; height: auto;">
</a>

**Telegram**
<a href="https://t.me/Wcowin" target="_blank">
<img src="https://pica.zhimg.com/80/v2-d5876bc0c8c756ecbba8ff410ed29c14_1440w.webp" style="width: 450px; height: auto;">
</a>

</center>

## 案例成果

- [Wcowin 的博客](https://wcowin.work) - Zensical 官方示例
- [更多案例敬请期待...](https://github.com/Wcowin/Zensical-Chinese-Tutorial)

## 贡献者

<a href="https://github.com/Wcowin/Zensical-Chinese-Tutorial/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Wcowin/Zensical-Chinese-Tutorial" />
</a>

[![Built with Zensical](https://img.shields.io/badge/Built_with-Zensical-4051B5?style=for-the-badge)](https://zensical.org/) 

## License

**MIT License**

Copyright (c) 2022-2025 Wang Kewen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
IN THE SOFTWARE.