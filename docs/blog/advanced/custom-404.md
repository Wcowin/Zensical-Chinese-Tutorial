---
title: 自定义 404 页面
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 高级主题
---

# 自定义 404 页面

> 为你的 Zensical 网站添加个性化的 404 错误页面

## 概述

Zensical 支持自定义 404 页面，当用户访问不存在的页面时，会显示你自定义的 404 页面。

## 方法一：使用模板覆盖（推荐）

### 第一步：配置 custom_dir

在 `zensical.toml` 中启用模板覆盖：

```toml
[project.theme]
custom_dir = "docs/overrides"
```

### 第二步：创建 404.html

在 `docs/overrides/` 目录下创建 `404.html` 文件：

```
docs/
└── overrides/
    └── 404.html
```

### 第三步：编写 404 页面

创建自定义的 404 页面，例如：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 - 页面不存在</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            text-align: center;
        }
        .container {
            max-width: 600px;
            padding: 2rem;
        }
        h1 {
            font-size: 8rem;
            margin: 0;
            line-height: 1;
        }
        h2 {
            font-size: 2rem;
            margin: 1rem 0;
        }
        p {
            font-size: 1.2rem;
            margin: 1rem 0;
        }
        a {
            color: white;
            text-decoration: underline;
        }
        a:hover {
            opacity: 0.8;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>404</h1>
        <h2>页面走丢了</h2>
        <p>抱歉，您访问的页面不存在。</p>
        <p><a href="/">返回首页</a></p>
    </div>
</body>
</html>
```

## 方法二：使用公益 404 页面

你也可以使用腾讯公益 404 页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="公益404页面是由腾讯公司员工志愿者自主发起的互联网公益活动。">
    <title>404 - 您访问的页面搞丢了</title>
    <script src="https://volunteer.cdn-go.cn/404/latest/404.js" rendertarget="404DlV"></script>
    <style>
        body {
            overflow-x: hidden;
            max-width: 100vw;
            margin: 0;
            padding: 0;
            background-color: rgba(0, 0, 0, 0);
            color: white;
            text-align: center;
        }
        .container {
            position: relative;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            max-width: 1600px;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .background-img {
            width: 100%;
            max-width: 1600px;
            filter: brightness(75%);
        }
        .content {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            width: 98vw;
            max-width: 1600px;
            text-align: center;
        }
        .content h1 {
            font-size: 128px;
            font-weight: 800;
            margin: 0;
        }
        .content p {
            font-size: 28px;
            margin: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <img class="background-img" alt="404!您要访问的页面走丢了!" src="https://volunteer.cdn-go.cn/404/latest/img/dream4school.jpg" />
        <div class="content">
            <h1>404 NOT Found</h1>
            <p>您访问的页面走丢在寻找梦想的路上了</p>
            <p>不过您还可以和腾讯志愿者一起</p>
            <p><b>为孩子们点亮一个梦想</b></p>
        </div>
    </div>
</body>
</html>
```

## 方法三：使用 Zensical 默认 404

如果你不创建自定义 404 页面，Zensical 会使用默认的 404 页面。

当然，你也可以选择在 Zensical 默认提供的 404 页面上进行修改。在 Zensiacl 默认提供的 404 页面上进行修改的方式属于本文[方法一：使用模板覆盖](#_2)的一种应用场景。

首先在 zensical.toml 中启用模板覆盖：

```
[project.theme]
custom_dir = "docs/overrides"
```

然后在 `docs/overrides/` 目录下创建 `404.html` 文件：

```
docs/
└── overrides/
    └── 404.html
```

zensical 官方提供的404 页面模板内容如下，请将其复制到 `404.html` 文件中。

```html
<!--
  Copyright (c) 2025 Zensical and contributors

  SPDX-License-Identifier: MIT
  Third-party contributions licensed under DCO
-->

{% extends "main.html" %}

<!-- Content -->
{% block content %}
  <h1>404 - Not found</h1>
{% endblock %}
```

你可以在 `{% block content %}` 内部编写 `html` 代码来实现页面自定义，例如：

```html
{% extends "main.html" %}

<!-- Content -->
{% block content %}
  <h1>404 - Not found</h1>
  <p>页面似乎走丢了，这里是自定义内容。</p>
  <p>在 content 内容块内进行模版覆盖。</p>
{% endblock %}
```

使用官方默认模板进行模板覆盖的好处是能够在 404 页面中保留站点原生的页眉、顶部导航栏与页脚。

## 部署配置

### Netlify

在 `netlify.toml` 中配置：

```toml
[[redirects]]
  from = "/*"
  to = "/404.html"
  status = 404
```

### GitHub Pages

GitHub Pages 会自动识别 `404.html` 文件。

### GitLab Pages

GitLab Pages 会自动识别 `404.html` 文件。

### EdgeOne Pages

EdgeOne Pages 会自动识别 `404.html` 文件。

### Nginx

在 Nginx 配置中添加：

```nginx
error_page 404 /404.html;
location = /404.html {
    root /var/www/your-site;
    internal;
}
```

## 注意事项

1. **文件位置**：404 页面必须放在 `docs/overrides/` 目录下
2. **文件名**：必须命名为 `404.html`
3. **完整 HTML**：404 页面必须是完整的 HTML 文档
4. **相对路径**：页面中的链接应使用相对路径或绝对路径

## 示例效果

自定义 404 页面可以：
- 显示友好的错误信息
- 提供返回首页的链接
- 展示网站导航
- 添加搜索功能
- 使用公益 404 页面

## 参考资源

- [Zensical 模板覆盖文档](https://zensical.org/docs/)
- [腾讯公益 404](https://volunteer.cdn-go.cn/404/)
- [Material for MkDocs 404 页面](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/#custom-404-page)

---

**提示**：创建 404 页面后，记得测试一下，确保页面能正常显示。

