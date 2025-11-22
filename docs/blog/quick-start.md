---
title: 5 分钟快速开始
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 快速开始
---

# 5 分钟快速开始 Zensical

> 从零到一，快速搭建你的 Zensical 博客

## 第一步：安装 Zensical

Zensical 是用 Rust 和 Python 编写的，以 Python 包的形式发布。推荐使用 Python 虚拟环境进行安装。

### 使用 pip 安装（推荐）

=== "macOS / Linux"

    ```bash
    # 创建虚拟环境
    python3 -m venv .venv
    
    # 激活虚拟环境
    source .venv/bin/activate
    
    # 安装 Zensical
    pip install zensical
    ```

=== "Windows"

    ```bash
    # 创建虚拟环境
    python3 -m venv .venv
    
    # 激活虚拟环境
    .venv\Scripts\activate
    
    # 安装 Zensical
    pip install zensical
    ```

### 使用 uv 安装（开发者推荐）

如果你是 Python 开发者，可能已经在使用 [uv](https://docs.astral.sh/uv/) 作为包管理器：

```bash
uv init
uv add zensical
```

## 第二步：创建项目

在你想要创建项目的目录中运行：

```bash
zensical new .
```

这将创建以下结构：

```
.
├─ .github/
├─ docs/
│  ├─ index.md
│  └─ markdown.md
└─ zensical.toml
```

!!! tip "使用模板项目"
    你也可以克隆本教程的模板项目快速开始：
    
    ```bash
    git clone https://github.com/Wcowin/Zensical-Wcowin.git my-blog
    cd my-blog
    pip install -r requirements.txt
    ```

## 第三步：配置项目

Zensical 提供了许多配置选项，都有合理的默认值。`site_name` 是唯一必需的设置：

```toml title="zensical.toml"
[project]
site_name = "我的博客"
```

强烈建议同时设置 `site_url`，这是以下功能的前提：

- 即时导航
- 即时预览
- 自定义错误页面

```toml title="zensical.toml"
[project]
site_name = "我的博客"
site_url = "https://example.com"
site_author = "你的名字"
site_description = "我的 Zensical 博客"

[project.theme]
language = "zh"  # 中文界面
```

## 第四步：启动开发服务器

Zensical 内置了 Web 服务器，可以在编写时实时预览。服务器会在你修改源文件时自动重建网站：

```bash
zensical serve
```

在浏览器中打开 [http://localhost:8000](http://localhost:8000) 即可看到你的网站。

## 第五步：创建第一篇文章

在 `docs/blog/posts/` 目录下创建文件 `2025-01-22-hello-world.md`：

```markdown
---
title: Hello World
date: 2025-01-22
authors:
  - name: 你的名字
    email: your@email.com
categories:
  - 开始
---

# Hello World

这是我的第一篇 Zensical 博客文章！

## 特点

- ✅ 简单易用
- ✅ 功能强大
- ✅ 性能优异

## 下一步

继续阅读 [博客系统完全指南](../blog-tutorial.md) 了解更多功能。
```

保存文件后，网站会自动刷新，你就能看到新文章了！

## 第六步：构建网站

当你完成编辑后，可以从 Markdown 文件构建静态网站：

```bash
zensical build
```

生成的文件将位于 `site/` 目录中，这些文件构成了你的项目文档。网站是完全独立的，不需要数据库或服务器。可以部署到 GitHub Pages、CDN 或你自己的 Web 空间。

## 完成！🎉

你已经成功创建了一个 Zensical 博客！

### 接下来可以做什么？

1. **编写更多文章** - 在 `docs/blog/posts/` 中添加更多 Markdown 文件
2. **自定义样式** - 修改 `docs/stylesheets/extra.css`
3. **添加页面** - 在 `docs/` 中创建新的 Markdown 文件
4. **部署到线上** - 参考部署指南

### 常用命令

```bash
# 启动开发服务器
zensical serve

# 构建静态网站
zensical build

# 查看帮助
zensical --help
```

### 推荐阅读

- [Zensical 博客系统完全指南](blog-tutorial.md)
- [项目配置详解](configuration.md)
- [主题定制指南](customization.md)

---

**遇到问题？** 查看 [FAQ](faq.md) 或访问 [Zensical 官方文档](https://zensical.org/docs/)
