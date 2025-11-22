# zensical.toml 配置详解

> 全面了解 Zensical 的配置选项

## 配置文件格式

Zensical 项目通过 `zensical.toml` 文件进行配置。如果你使用 `zensical new` 命令创建项目，该文件会自动生成，并包含带注释的示例配置。

### 为什么选择 TOML？

[TOML 文件格式](https://toml.io/) 专门设计为易于扫描和理解。我们选择 TOML 而不是 YAML，因为它避免了 YAML 的一些问题：

- **YAML 使用缩进表示结构**，这使得缩进错误特别容易出现且难以定位。在 TOML 中，空白主要是样式选择。
- **在 YAML 中，值不需要转义**，这可能导致歧义，例如 `no` 可能被解释为字符串或布尔值。TOML 要求所有字符串都要加引号。

## 从 MkDocs 过渡

为了便于从 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 过渡，Zensical 可以原生读取 `mkdocs.yml` 配置文件。但是，我们建议新项目使用 `zensical.toml` 文件。

!!! info "配置文件支持"
    由于 Zensical 是由 Material for MkDocs 的创建者构建的，我们支持通过 `mkdocs.yml` 文件进行配置，作为过渡机制，使现有项目能够平滑迁移到 Zensical。对 `mkdocs.yml` 的支持将始终保持，但最终会移出核心。

## 项目作用域

`zensical.toml` 配置以声明项目作用域的行开始：

```toml
[project]
```

目前，所有设置都包含在此作用域内。随着 Zensical 的发展，我们将引入额外的作用域，并在适当的地方将设置移出项目作用域。当然，我们会提供自动重构，因此无需手动迁移。

## 主题变体

Zensical 提供两种主题变体：**modern**（现代）和 **classic**（经典），默认为 modern。classic 主题完全匹配 Material for MkDocs 的外观和感觉，而 modern 主题提供全新的设计。

如果你来自 Material for MkDocs 并希望保持其外观，或基于其外观自定义网站，可以切换到 classic 主题变体：

=== "zensical.toml"

    ```toml
    [project.theme]
    variant = "classic"
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      variant: classic
    ```

!!! tip "自定义提示"
    Zensical 的 HTML 结构在两种主题变体中都与 Material for MkDocs 匹配。这意味着你现有的 CSS 和 JavaScript 自定义应该可以在任一主题变体中工作。

## 基础设置

### site_name

**必需设置** - 提供网站名称，将包含在 HTML head 和页面标题中。

=== "zensical.toml"

    ```toml
    [project]
    site_name = "我的 Zensical 项目"
    ```

=== "mkdocs.yml"

    ```yaml
    site_name: 我的 Zensical 项目
    ```

!!! note "关于 site_name"
    `site_name` 目前是必需的，因为 Zensical 替换的静态网站生成器 MkDocs 需要它。我们计划在未来版本中使此设置可选。

### site_url

指定网站的规范 URL，将出现在 HTML 头部。除非你正在构建离线使用的文档，否则应该设置此项。

=== "zensical.toml"

    ```toml
    [project]
    site_url = "https://example.com"
    ```

=== "mkdocs.yml"

    ```yaml
    site_url: https://example.com
    ```

!!! warning "重要"
    设置 `site_url` 是以下功能的前提：
    
    - 即时导航
    - 即时预览
    - 自定义错误页面

### site_description

用于 HTML head 中的网站描述（如果页面本身未在页面元数据中指定描述）。一些搜索引擎使用此描述来描述页面内容。

=== "zensical.toml"

    ```toml
    [project]
    site_description = "这是我的 Zensical 文档网站"
    ```

=== "mkdocs.yml"

    ```yaml
    site_description: 这是我的 Zensical 文档网站
    ```

### site_author

用于 HTML head 元素中，指示网站的作者。

=== "zensical.toml"

    ```toml
    [project]
    site_author = "张三"
    ```

=== "mkdocs.yml"

    ```yaml
    site_author: 张三
    ```

### copyright

指定将插入到页面页脚的版权声明。可以在此处指定 HTML 片段或纯文本。

=== "zensical.toml"

    ```toml
    [project]
    copyright = "&copy; 2025 张三"
    ```

=== "mkdocs.yml"

    ```yaml
    copyright: "&copy; 2025 张三"
    ```

### docs_dir

指定包含源文件的目录路径。必须是相对路径，相对于配置文件解析。

=== "zensical.toml"

    ```toml
    [project]
    docs_dir = "docs"
    ```

=== "mkdocs.yml"

    ```yaml
    docs_dir: docs
    ```

### site_dir

指定网站将写入的目录路径。必须是相对路径，相对于配置文件解析。

=== "zensical.toml"

    ```toml
    [project]
    site_dir = "site"
    ```

=== "mkdocs.yml"

    ```yaml
    site_dir: site
    ```

### extra

`extra` 配置选项用于存储模板使用的任意键值对。如果你覆盖模板，可以使用这些值来自定义行为。

=== "zensical.toml"

    ```toml
    [project.extra]
    key = "value"
    analytics = "UA-XXXXXXXX-X"
    ```

=== "mkdocs.yml"

    ```yaml
    extra:
      key: value
      analytics: UA-XXXXXXXX-X
    ```

### use_directory_urls

控制文档网站的目录结构，从而控制用于链接到页面的 URL 格式。

=== "zensical.toml"

    ```toml
    [project]
    use_directory_urls = true  # 默认值
    ```

=== "mkdocs.yml"

    ```yaml
    use_directory_urls: true
    ```

!!! info "离线使用"
    在构建离线使用时，此选项会自动设置为 `false`，以便可以从本地文件系统浏览文档，而无需 Web 服务器。

## 主题配置

### language

设置网站的语言。

=== "zensical.toml"

    ```toml
    [project.theme]
    language = "zh"  # 中文
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      language: zh
    ```

### features

启用或禁用主题功能。

=== "zensical.toml"

    ```toml
    [project.theme]
    features = [
        "navigation.instant",           # 即时导航
        "navigation.instant.prefetch",  # 预加载
        "navigation.tracking",          # 锚点跟踪
        "navigation.tabs",              # 导航标签
        "navigation.sections",          # 导航部分
        "navigation.expand",            # 展开导航
        "navigation.top",               # 返回顶部按钮
        "search.suggest",               # 搜索建议
        "search.highlight",             # 搜索高亮
        "content.code.copy",            # 代码复制按钮
    ]
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      features:
        - navigation.instant
        - navigation.instant.prefetch
        - navigation.tracking
        - navigation.tabs
        - navigation.sections
        - navigation.expand
        - navigation.top
        - search.suggest
        - search.highlight
        - content.code.copy
    ```

### palette

配置颜色主题。

=== "zensical.toml"

    ```toml
    [[project.theme.palette]]
    scheme = "default"
    primary = "indigo"
    accent = "indigo"
    
    [[project.theme.palette]]
    scheme = "slate"
    primary = "indigo"
    accent = "indigo"
    toggle = { icon = "material/brightness-4", name = "切换到深色模式" }
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      palette:
        - scheme: default
          primary: indigo
          accent: indigo
        - scheme: slate
          primary: indigo
          accent: indigo
          toggle:
            icon: material/brightness-4
            name: 切换到深色模式
    ```

### font

配置字体。

=== "zensical.toml"

    ```toml
    [project.theme.font]
    text = "Roboto"
    code = "Roboto Mono"
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      font:
        text: Roboto
        code: Roboto Mono
    ```

### logo 和 favicon

设置网站 logo 和 favicon。

=== "zensical.toml"

    ```toml
    [project.theme]
    logo = "assets/logo.png"
    favicon = "assets/favicon.png"
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      logo: assets/logo.png
      favicon: assets/favicon.png
    ```

## 插件配置

### 博客插件

=== "zensical.toml"

    ```toml
    [project.plugins.blog]
    enabled = true
    blog_dir = "blog"
    post_date_format = "full"
    post_url_format = "{date}/{slug}"
    post_readtime = true
    post_readtime_words_per_minute = 265
    draft = true
    ```

=== "mkdocs.yml"

    ```yaml
    plugins:
      - blog:
          enabled: true
          blog_dir: blog
          post_date_format: full
          post_url_format: "{date}/{slug}"
          post_readtime: true
          post_readtime_words_per_minute: 265
          draft: true
    ```

### 搜索插件

=== "zensical.toml"

    ```toml
    [project.plugins.search]
    enabled = true
    lang = ["zh", "en"]
    separator = '[\s\-\.]+'
    ```

=== "mkdocs.yml"

    ```yaml
    plugins:
      - search:
          enabled: true
          lang:
            - zh
            - en
          separator: '[\s\-\.]+'
    ```

### 标签插件

=== "zensical.toml"

    ```toml
    [project.plugins.tags]
    enabled = true
    tags_file = "tags.md"
    ```

=== "mkdocs.yml"

    ```yaml
    plugins:
      - tags:
          enabled: true
          tags_file: tags.md
    ```

## 导航配置

### nav

定义网站的导航结构。

=== "zensical.toml"

    ```toml
    [[project.nav]]
    Home = "index.md"
    
    [[project.nav]]
    "快速开始" = "quick-start.md"
    
    [[project.nav]]
    "配置" = "configuration.md"
    
    [[project.nav.Blog]]
    "博客" = "blog/index.md"
    ```

=== "mkdocs.yml"

    ```yaml
    nav:
      - Home: index.md
      - 快速开始: quick-start.md
      - 配置: configuration.md
      - Blog:
          - 博客: blog/index.md
    ```

## Markdown 扩展

### 启用扩展

=== "zensical.toml"

    ```toml
    [project.markdown_extensions]
    pymdownx.highlight = { anchor_linenums = true }
    pymdownx.superfences = {}
    pymdownx.tabbed = { alternate_style = true }
    pymdownx.tasklist = { custom_checkbox = true }
    admonition = {}
    attr_list = {}
    md_in_html = {}
    ```

=== "mkdocs.yml"

    ```yaml
    markdown_extensions:
      - pymdownx.highlight:
          anchor_linenums: true
      - pymdownx.superfences
      - pymdownx.tabbed:
          alternate_style: true
      - pymdownx.tasklist:
          custom_checkbox: true
      - admonition
      - attr_list
      - md_in_html
    ```

## 完整配置示例

```toml title="zensical.toml"
[project]
site_name = "我的 Zensical 博客"
site_url = "https://example.com"
site_author = "张三"
site_description = "使用 Zensical 构建的现代文档网站"
copyright = "&copy; 2025 张三"

[project.theme]
variant = "modern"
language = "zh"
logo = "assets/logo.png"
favicon = "assets/favicon.png"

features = [
    "navigation.instant",
    "navigation.instant.prefetch",
    "navigation.tracking",
    "navigation.tabs",
    "navigation.sections",
    "navigation.top",
    "search.suggest",
    "search.highlight",
    "content.code.copy",
]

[[project.theme.palette]]
scheme = "default"
primary = "indigo"
accent = "indigo"

[[project.theme.palette]]
scheme = "slate"
primary = "indigo"
accent = "indigo"

[project.theme.font]
text = "Roboto"
code = "Roboto Mono"

[project.plugins.blog]
enabled = true
blog_dir = "blog"
post_date_format = "full"
post_readtime = true
post_readtime_words_per_minute = 265

[project.plugins.search]
enabled = true
lang = ["zh", "en"]

[project.plugins.tags]
enabled = true

[project.markdown_extensions]
pymdownx.highlight = { anchor_linenums = true }
pymdownx.superfences = {}
pymdownx.tabbed = { alternate_style = true }
pymdownx.tasklist = { custom_checkbox = true }
admonition = {}
attr_list = {}
md_in_html = {}

[[project.nav]]
Home = "index.md"

[[project.nav]]
"快速开始" = "quick-start.md"

[[project.nav]]
"配置" = "configuration.md"

[[project.nav.Blog]]
"博客" = "blog/index.md"
```

## 下一步

- 了解 [主题定制](theme-customization.md)
- 学习 [博客系统](blog-tutorial.md)
- 查看 [部署指南](deployment/netlify.md)

---

**参考资料**：[Zensical 官方文档 - Basics](https://zensical.org/docs/setup/basics/)
