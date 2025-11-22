---
title: 搜索插件配置
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 插件系统
---

# 搜索插件配置

> Zensical 内置的强大搜索功能

## 基本配置

在 `zensical.toml` 中配置搜索插件：

```toml
[project.plugins.search]
separator = '[\s\u200b\-]'  # 搜索分隔符
lang = ["zh", "en"]        # 支持的语言
```

## 主题功能

在主题中启用搜索功能：

```toml
[project.theme]
features = [
    "search.suggest",    # 搜索建议
    "search.highlight",  # 搜索结果高亮
    "search.share",      # 搜索结果分享
]
```

## 中文搜索优化

对于中文内容，推荐使用以下配置：

```toml
[project.plugins.search]
separator = '[\s\u200b\-\uff0c\u3002\uff1f\uff01]+'  # 中文标点符号
lang = ["zh"]  # 中文
```
