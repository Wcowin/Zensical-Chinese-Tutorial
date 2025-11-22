---
title: 主题定制指南
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 主题定制
---

# 主题定制指南

> 详细的 Zensical 主题定制教程

## 主题变体

Zensical 提供两种主题变体：

### Modern 主题（推荐）

```toml
[project.theme]
variant = "modern"
```

全新的现代化设计，更美观、更流畅。

### Classic 主题

```toml
[project.theme]
variant = "classic"
```

与 Material for MkDocs 完全一致的外观，适合从 MkDocs 迁移的项目。

## 颜色配置

### 调色板配置

Zensical 支持明暗主题切换和自定义颜色：

```toml
# 自动模式（跟随系统）
[[project.theme.palette]]
media = "(prefers-color-scheme)"
toggle = { icon = "material/link", name = "关闭自动模式" }

# 日间模式
[[project.theme.palette]]
media = "(prefers-color-scheme: light)"
scheme = "default"                # 日间模式配色
primary = "indigo"                # 主色调
accent = "indigo"                 # 强调色
toggle = { icon = "material/toggle-switch", name = "切换至夜间模式" }

# 夜间模式
[[project.theme.palette]]
media = "(prefers-color-scheme: dark)"
scheme = "slate"                  # 夜间模式配色
primary = "indigo"                # 主色调
accent = "indigo"                 # 强调色
toggle = { icon = "material/toggle-switch-off-outline", name = "切换至日间模式" }
```

### 支持的主色调

Zensical 支持以下主色调：

- `red` - 红色
- `pink` - 粉色
- `purple` - 紫色
- `deep-purple` - 深紫色
- `indigo` - 靛蓝色（推荐）
- `blue` - 蓝色
- `light-blue` - 浅蓝色
- `cyan` - 青色
- `teal` - 青绿色
- `green` - 绿色
- `light-green` - 浅绿色
- `lime` - 酸橙色
- `yellow` - 黄色
- `amber` - 琥珀色
- `orange` - 橙色
- `deep-orange` - 深橙色
- `brown` - 棕色
- `grey` - 灰色
- `blue-grey` - 蓝灰色
- `black` - 黑色
- `white` - 白色

### 自定义颜色

在 `docs/stylesheets/extra.css` 中使用 CSS 变量：

```css
:root {
  --md-primary-fg-color: #4051B5;
  --md-accent-fg-color: #536DFE;
}
```

## 功能配置

### 导航功能

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
    "navigation.footer",            # 页脚导航
]
```

### 搜索功能

```toml
features = [
    "search.suggest",               # 搜索建议
    "search.highlight",             # 搜索高亮
    "search.share",                 # 搜索分享
]
```

### 内容功能

```toml
features = [
    "content.tooltips",             # 内容提示框
    "content.code.copy",            # 代码复制按钮
    "content.code.select",          # 代码选择功能
    "content.code.annotate",        # 代码注释功能
]
```

## 图标配置

```toml
[project.theme.icon]
repo = "fontawesome/brands/github"          # 仓库图标
previous = "fontawesome/solid/angle-left"   # 上一页图标
next = "fontawesome/solid/angle-right"     # 下一页图标
alternate = "fontawesome/solid/language"   # 语言切换图标
```

## Logo 和 Favicon

```toml
[project.theme]
logo = "assets/logo.svg"           # 网站 Logo
favicon = "assets/favicon.png"     # 网站图标
```

## 模板覆盖

### 启用模板覆盖

```toml
[project.theme]
custom_dir = "docs/overrides"
```

### 目录结构

```
docs/
└── overrides/
    ├── 404.html                  # 自定义 404 页面
    ├── main.html                 # 主模板
    └── partials/
        ├── comments.html         # 评论系统
        ├── footer.html           # 页脚
        └── header.html           # 页头
```

## 自定义样式

### 添加自定义 CSS

在 `zensical.toml` 中：

```toml
extra_css = [
    "stylesheets/extra.css",
]
```

在 `docs/stylesheets/extra.css` 中编写样式：

```css
/* 自定义样式 */
.md-header {
    background-color: #4051B5;
}

/* 响应式设计 */
@media (max-width: 768px) {
    .md-header {
        padding: 0.5rem;
    }
}
```

### 添加自定义 JavaScript

在 `zensical.toml` 中：

```toml
extra_javascript = [
    "javascripts/extra.js",
]
```

在 `docs/javascripts/extra.js` 中编写脚本：

```javascript
// 即时导航兼容
document$.subscribe(function() {
    // 你的代码
});
```

## 高级定制

### 自定义字体

参考 [自定义字体指南](../blog/advanced/custom-fonts.md)

### 自定义 404 页面

参考 [自定义 404 页面](../blog/advanced/custom-404.md)

### 添加评论系统

参考 [添加评论系统](../blog/advanced/comment-system.md)

## 完整配置示例

```toml
[project.theme]
variant = "modern"
custom_dir = "docs/overrides"
logo = "assets/logo.svg"
favicon = "assets/favicon.png"
language = "zh"

features = [
    "navigation.instant",
    "navigation.tracking",
    "navigation.tabs",
    "navigation.sections",
    "navigation.top",
    "search.suggest",
    "search.highlight",
    "content.code.copy",
]

[[project.theme.palette]]
media = "(prefers-color-scheme: light)"
scheme = "default"
primary = "indigo"
accent = "indigo"

[[project.theme.palette]]
media = "(prefers-color-scheme: dark)"
scheme = "slate"
primary = "indigo"
accent = "indigo"

[project.theme.icon]
repo = "fontawesome/brands/github"
```

## 参考资源

- [Zensical 官方文档](https://zensical.org/docs/)
- [Material for MkDocs 主题配置](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/)
- [Font Awesome 图标](https://fontawesome.com/icons)

---

**提示**：主题定制可以让你的网站更加个性化！
