---
title: 标签插件使用
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 插件系统
---

# 标签插件使用

> 使用标签系统组织和分类你的文档内容

!!! info "功能状态"
    标签功能是 Zensical Feature Parity 的一部分，将作为原生功能提供。

## 什么是标签系统？

标签系统允许你为文章添加关键词标签，方便读者按主题浏览内容：

- ✅ **内容分类** - 按主题组织文章
- ✅ **快速导航** - 点击标签查看相关文章
- ✅ **自动索引** - 自动生成标签页面

## 基本配置

在 `zensical.toml` 中启用标签插件：

```toml
[project.plugins.tags]
```

### 配置选项

```toml
[project.plugins.tags]
tags_file = "tags.md"        # 标签索引页面
```

## 使用方法

### 为文章添加标签

在文章的 front matter 中添加 `tags` 字段：

```markdown
---
title: Python 装饰器详解
date: 2025-01-22
tags:
  - Python
  - 装饰器
  - 高级特性
  - 函数式编程
---

# Python 装饰器详解

文章内容...
```

### 创建标签索引页面

创建 `docs/tags.md` 文件：

```markdown
---
title: 标签
hide:
  - toc
---

# 标签

<!-- 标签列表会自动生成 -->
```

### 在导航中添加标签页

```toml
nav = [
    { "主页" = "index.md" },
    { "标签" = "tags.md" },
    # ... 其他导航项
]
```

## 标签命名规范

### 推荐做法

- ✅ 使用简洁明了的标签名
- ✅ 保持标签命名一致性
- ✅ 使用常见术语
- ✅ 控制标签数量（每篇 3-5 个）

### 避免做法

- ❌ 使用过长的标签名
- ❌ 同一概念使用多个标签（如 "JS" 和 "JavaScript"）
- ❌ 使用过于宽泛的标签
- ❌ 每篇文章添加过多标签

## 标签示例

### 技术博客标签

```yaml
tags:
  - Python
  - JavaScript
  - Web 开发
  - 数据库
  - API
  - 教程
  - 最佳实践
```

### 文档项目标签

```yaml
tags:
  - 快速开始
  - 配置
  - 部署
  - 故障排除
  - API 参考
  - 示例
```

## 标签与分类的区别

| 特性 | 标签 (Tags) | 分类 (Categories) |
|------|-------------|-------------------|
| **数量** | 可以有多个 | 通常 1-2 个 |
| **层级** | 扁平结构 | 可以有层级 |
| **用途** | 细粒度分类 | 主题分类 |
| **示例** | Python, 装饰器, 教程 | 技术, 生活 |

### 同时使用标签和分类

```markdown
---
title: Python 装饰器详解
date: 2025-01-22
categories:
  - 技术
  - Python
tags:
  - 装饰器
  - 函数式编程
  - 高级特性
---
```

## 自定义标签样式

在 `docs/stylesheets/extra.css` 中自定义标签样式：

```css
/* 标签基础样式 */
.md-tag {
    background-color: var(--md-primary-fg-color);
    color: white;
    padding: 0.2rem 0.5rem;
    border-radius: 0.25rem;
    font-size: 0.75rem;
    margin-right: 0.25rem;
}

/* 标签悬停效果 */
.md-tag:hover {
    opacity: 0.8;
}

/* 特定标签颜色 */
.md-tag[data-tag="Python"] {
    background-color: #3776ab;
}

.md-tag[data-tag="JavaScript"] {
    background-color: #f7df1e;
    color: black;
}
```

## 常见问题

### 标签页面不显示

**问题**：创建了 tags.md 但标签不显示

**解决方案**：

1. 确保 `[project.plugins.tags]` 已配置
2. 检查 `tags_file` 路径是否正确
3. 确保文章中有 `tags` 字段
4. 重新构建网站

### 标签链接 404

**问题**：点击标签链接出现 404

**解决方案**：

1. 检查 `site_url` 配置
2. 确保标签页面存在
3. 清理并重新构建：`zensical build --clean`

## 参考资源

- [Zensical 官方文档](https://zensical.org/docs/)
- [博客系统完全指南](../../tutorials/blog-tutorial.md)

---

**提示**：合理使用标签可以大大提升内容的可发现性！
