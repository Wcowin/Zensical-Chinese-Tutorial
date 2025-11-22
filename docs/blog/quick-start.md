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

```bash
# 使用 pip 安装
pip install zensical
```

## 第二步：创建项目

```bash
# 方法 1：使用 zensical 命令创建
zensical new my-blog
cd my-blog

# 方法 2：克隆模板（推荐）
git clone https://github.com/Wcowin/Zensical-Wcowin.git my-blog
cd my-blog
pip install -r requirements.txt
```

## 第三步：启动本地服务

```bash
zensical serve
```

打开浏览器访问 `http://127.0.0.1:8000`

## 第四步：创建第一篇文章

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

## 第五步：自定义网站

编辑 `zensical.toml` 修改网站信息：

```toml
[project]
site_name = "我的博客"
site_url = "https://example.com"
site_author = "你的名字"

[project.theme]
language = "zh"  # 中文
```

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
