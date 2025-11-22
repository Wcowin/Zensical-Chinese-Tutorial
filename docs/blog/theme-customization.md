---
title: 主题定制指南
date: 2025-01-22
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

与 Material for MkDocs 完全一致的外观。

## 自定义颜色

在 `docs/stylesheets/extra.css` 中定义：

```css
:root {
  --md-primary-fg-color: #4051B5;
  --md-accent-fg-color: #536DFE;
}
```

## 更多内容

详细内容正在完善中...
