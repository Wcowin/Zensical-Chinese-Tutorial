---
title: 博客插件详解
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 插件系统
---

# 博客插件详解

> Zensical 内置的强大博客系统

## 什么是博客插件？

Zensical 内置了功能强大的博客插件，无需额外安装：

- ✅ **开箱即用** - 无需额外安装
- ✅ **自动索引** - 自动生成博客列表
- ✅ **分类标签** - 支持分类和标签
- ✅ **阅读时间** - 自动计算阅读时间
- ✅ **草稿功能** - 支持草稿管理
- ✅ **作者信息** - 显示作者和日期

## 基本配置

在 `zensical.toml` 中启用博客插件：

```toml
[project.plugins.blog]
post_date_format = "full"                    # 日期格式
draft = true                                  # 启用草稿
post_readtime = true                          # 显示阅读时间
post_readtime_words_per_minute = 265          # 每分钟阅读字数（中文适配）
post_url_format = "{date}/{slug}"             # 文章 URL 格式
pagination_per_page = 10                      # 每页显示文章数
pagination_url_format = "page/{page}"         # 分页 URL 格式
```

## 创建博客文章

在 `docs/blog/posts/` 目录下创建 Markdown 文件：

```markdown
---
title: 我的第一篇博客
date: 2025-01-22
authors:
  - name: 你的名字
    email: your@email.com
categories:
  - 技术
  - Python
tags:
  - Zensical
  - 教程
---

# 我的第一篇博客

这是文章内容...
```

## 配置选项详解

### post_date_format

日期显示格式：

- `full` - 完整日期（如：2025年1月22日）
- `short` - 简短格式（如：2025-01-22）
- `medium` - 中等格式

### post_readtime

自动计算阅读时间：

```toml
post_readtime = true
post_readtime_words_per_minute = 265  # 中文适配
```

### draft

草稿功能：

```toml
draft = true                    # 启用草稿
draft_if_future_date = true     # 未来日期自动标记为草稿
```

更多详细内容请参考 [博客系统完全指南](../blog-tutorial.md)。
