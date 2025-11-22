---
title: zensical.toml 配置详解
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 配置
  - 教程
---

# zensical.toml 配置详解

> 完整的 Zensical 配置文件说明

## 文件结构

`zensical.toml` 是 Zensical 的核心配置文件，使用 TOML 格式。

## 基本配置

### 项目信息

```toml
[project]
# 网站名称（必需）
site_name = "我的博客"

# 网站 URL（强烈推荐）
site_url = "https://example.com"

# 网站作者
site_author = "你的名字"

# 网站描述
site_description = "一个关于技术和生活的博客"

# 版权信息
copyright = "Copyright (c) 2025 Your Name"
```

## 主题配置

### 主题设置

```toml
[project.theme]
# 主题变体（Zensical 特有）
variant = "modern"

# 自定义模板目录（相对于配置文件）
custom_dir = "overrides"

# 网站 Logo
logo = "https://example.com/logo.png"

# 网站 Favicon
favicon = "https://example.com/favicon.ico"

# 界面语言
language = "zh"

# 主题名称（如果使用 Material for MkDocs）
# name = "material"
```

### 主题特性

```toml
[project.theme]
features = [
    # 导航相关
    "announce.dismiss",           # 可关闭公告栏
    "navigation.prune",           # 只渲染可见导航项
    "navigation.tracking",        # 滚动时 URL 锚点自动更新
    "navigation.tabs",            # 一级导航显示为顶部 Tab
    "navigation.sections",        # 侧边栏分组
    "navigation.top",             # 返回顶部按钮
    "navigation.footer",          # 上一页/下一页导航
    "navigation.expand",          # 默认展开导航
    "navigation.indexes",         # 章节索引页
    
    # 搜索相关
    "search.suggest",             # 搜索建议
    "search.highlight",           # 搜索结果高亮
    "search.share",               # 搜索结果分享
    
    # 目录相关
    "toc.follow",                 # 目录跟随滚动
    
    # 内容相关
    "content.tooltips",           # 内容提示框
    "content.code.copy",          # 代码复制按钮
    "content.code.select",        # 代码选择功能
    "content.code.annotate",      # 代码注释功能
]
```

### 调色板配置

```toml
# 自动模式
[[project.theme.palette]]
media = "(prefers-color-scheme)"
toggle = { icon = "material/link", name = "关闭自动模式" }

# 日间模式
[[project.theme.palette]]
media = "(prefers-color-scheme: light)"
scheme = "default"
primary = "custom"
accent = "indigo"
toggle = { icon = "material/toggle-switch", name = "切换至夜间模式" }

# 夜间模式
[[project.theme.palette]]
media = "(prefers-color-scheme: dark)"
scheme = "slate"
primary = "custom"
accent = "indigo"
toggle = { icon = "material/toggle-switch-off-outline", name = "切换至日间模式" }
```

### 图标配置

```toml
[project.theme.icon]
# 仓库图标
repo = "fontawesome/brands/github"

# 上一页图标
previous = "fontawesome/solid/angle-left"

# 语言切换图标
alternate = "fontawesome/solid/language"
```

## 导航配置

```toml
nav = [
    { "主页" = "index.md" },
    { "技术" = [
        "blog/index.md",
        { "博客系统" = "blog-tutorial.md" },
        { "配置详解" = "configuration.md" },
    ]},
    { "关于" = "about.md" },
]
```

## 插件配置

### 搜索插件

```toml
[project.plugins.search]
# 搜索分隔符
separator = '[\s\u200b\-]'
```

### 博客插件

```toml
[project.plugins.blog]
# 日期格式：full（完整）、medium（中等）、short（简短）
post_date_format = "full"

# 启用草稿功能
draft = true

# 自动将未来日期的文章标记为草稿
draft_if_future_date = true

# 显示阅读时间
post_readtime = true

# 每分钟阅读字数（中文推荐 265）
post_readtime_words_per_minute = 265

# 文章 URL 格式
post_url_format = "{date}/{slug}"

# 分页设置
pagination_per_page = 5
pagination_url_format = "page/{page}"
```

### 标签插件

```toml
[project.plugins.tags]
# 标签插件配置
```

### 文档日期插件

```toml
[project.plugins."document-dates"]
# 显示位置：bottom（文档末尾）或 top（标题后）
position = "bottom"

# 日期类型：date（日期）、datetime（日期时间）、timeago（相对时间）
type = "date"

# 本地化语言
locale = "zh"

# 日期格式
date_format = "%Y-%m-%d"

# 时间格式
time_format = "%H:%M:%S"

# 显示作者信息
show_author = true
```

### RSS 插件

```toml
[project.plugins.rss]
# RSS 配置
```

## 额外资源

### 自定义 CSS

```toml
extra_css = [
    "stylesheets/extra.css",
    "stylesheets/custom.css",
]
```

### 自定义 JavaScript

```toml
extra_javascript = [
    "javascripts/extra.js",
    "javascripts/custom.js",
]
```

## 额外配置

### 基本设置

```toml
[project.extra]
# 显示生成器信息
generator = true
```

### 状态标签

```toml
[project.extra.status]
new = "最近添加"
deprecated = "已弃用"
```

### 多语言配置

```toml
[[project.extra.alternate]]
name = "中文"
link = "javascript:translateTo('chinese_simplified');"
lang = "zh"

[[project.extra.alternate]]
name = "English"
link = "javascript:translateTo('english');"
lang = "en"
```

### 社交媒体链接

```toml
[[project.extra.social]]
icon = "fontawesome/brands/github"
link = "https://github.com/yourusername"
name = "GitHub"

[[project.extra.social]]
icon = "fontawesome/brands/twitter"
link = "https://twitter.com/yourusername"
name = "Twitter"

[[project.extra.social]]
icon = "fontawesome/regular/envelope"
link = "mailto:your@email.com"
name = "Email"
```

### Google Analytics

```toml
[project.extra.analytics]
provider = "google"
property = "G-XXXXXXXXXX"

# 用户反馈配置
[project.extra.analytics.feedback]
title = "此页面有帮助吗？"

[[project.extra.analytics.feedback.ratings]]
icon = "material/thumb-up-outline"
name = "This page was helpful"
data = 1
note = "谢谢你的反馈！"

[[project.extra.analytics.feedback.ratings]]
icon = "material/thumb-down-outline"
name = "This page could be improved"
data = 0
note = "感谢您的反馈！"
```

## Markdown 扩展

### 基础扩展

```toml
[project.markdown_extensions]
# 缩写
abbr = {}

# 属性列表
attr_list = {}

# 警告框
admonition = {}

# 定义列表
def_list = {}

# 脚注
footnotes = {}

# 在 HTML 中使用 Markdown
md_in_html = {}

# 表格
tables = {}
```

### PyMdown 扩展

```toml
[project.markdown_extensions."pymdownx.betterem"]
smart_enable = "all"

[project.markdown_extensions."pymdownx.caret"]

[project.markdown_extensions."pymdownx.critic"]

[project.markdown_extensions."pymdownx.details"]

[project.markdown_extensions."pymdownx.emoji"]
emoji_index = "pymdownx.emoji.twemoji"
emoji_generator = "pymdownx.emoji.to_svg"

[project.markdown_extensions."pymdownx.inlinehilite"]

[project.markdown_extensions."pymdownx.keys"]

[project.markdown_extensions."pymdownx.mark"]

[project.markdown_extensions."pymdownx.smartsymbols"]

[project.markdown_extensions."pymdownx.superfences"]
custom_fences = [
    { name = "mermaid", class = "mermaid", format = "!!python/name:pymdownx.superfences.fence_code_format" }
]

[project.markdown_extensions."pymdownx.tabbed"]
alternate_style = true

[project.markdown_extensions."pymdownx.tilde"]

[project.markdown_extensions."pymdownx.magiclink"]

[project.markdown_extensions."pymdownx.blocks.caption"]
```

### 其他扩展

```toml
[project.markdown_extensions.toc]
permalink = true
title = "目录"

[project.markdown_extensions.highlight]
use_pygments = true
pygments_style = "material"

[project.markdown_extensions.arithmatex]
block_tag = "div"
```

## 完整示例

```toml
[project]
site_name = "我的博客"
site_url = "https://example.com"
site_author = "你的名字"
site_description = "一个关于技术和生活的博客"
copyright = "Copyright (c) 2025 Your Name"

[project.theme]
variant = "modern"
custom_dir = "overrides"
logo = "https://example.com/logo.png"
favicon = "https://example.com/favicon.ico"
language = "zh"

features = [
    "announce.dismiss",
    "navigation.tabs",
    "navigation.sections",
    "search.suggest",
    "search.highlight",
]

[[project.theme.palette]]
media = "(prefers-color-scheme)"
toggle = { icon = "material/link", name = "关闭自动模式" }

[[project.theme.palette]]
media = "(prefers-color-scheme: light)"
scheme = "default"
primary = "custom"
accent = "indigo"

[[project.theme.palette]]
media = "(prefers-color-scheme: dark)"
scheme = "slate"
primary = "custom"
accent = "indigo"

[project.theme.icon]
repo = "fontawesome/brands/github"

nav = [
    { "主页" = "index.md" },
    { "博客" = "blog/index.md" },
    { "关于" = "about.md" },
]

[project.plugins.search]
separator = '[\s\u200b\-]'

[project.plugins.blog]
post_date_format = "full"
draft = true
post_readtime = true
post_readtime_words_per_minute = 265
post_url_format = "{date}/{slug}"
pagination_per_page = 5

[project.extra]
generator = true

[[project.extra.social]]
icon = "fontawesome/brands/github"
link = "https://github.com/yourusername"

extra_css = ["stylesheets/extra.css"]
extra_javascript = ["javascripts/extra.js"]

[project.markdown_extensions]
abbr = {}
attr_list = {}
admonition = {}
tables = {}
```

## 常见问题

### Q: 如何修改主题颜色？

A: 在 `docs/stylesheets/extra.css` 中定义 CSS 变量：

```css
:root {
  --md-primary-fg-color: #518FC1;
  --md-primary-fg-color--light: #518FC1;
  --md-primary-fg-color--dark: #518FC1;
}
```

### Q: 如何禁用某个功能？

A: 在 `features` 列表中注释掉对应的功能，或从 `[project.plugins]` 中删除插件配置。

### Q: 如何添加自定义字体？

A: 在 `extra_css` 中添加字体文件，然后在 CSS 中使用。

---

**更多信息：** 访问 [Zensical 官方文档](https://zensical.org/docs/setup/basics/)
