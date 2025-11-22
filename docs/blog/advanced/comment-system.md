---
title: 添加评论系统
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 高级主题
---

# 添加评论系统

> 为你的 Zensical 网站添加评论功能

## 概述

Zensical 支持通过模板覆盖添加评论系统。本文介绍如何使用 **Giscus**（基于 GitHub Discussions）添加评论功能。

## 为什么选择 Giscus？

Giscus 是一个基于 GitHub Discussions 的评论系统：

- ✅ **开源免费** - 完全开源，永久免费
- ✅ **无跟踪无广告** - 保护用户隐私
- ✅ **无需数据库** - 所有数据存储在 GitHub Discussions
- ✅ **自动同步** - 自动从 GitHub 拉取新评论
- ✅ **支持主题** - 自动适配明暗主题
- ✅ **多语言支持** - 支持多种语言

## 配置步骤

### 第一步：启用模板覆盖

在 `zensical.toml` 中配置：

```toml
[project.theme]
custom_dir = "docs/overrides"
```

### 第二步：创建目录结构

创建以下目录结构：

```
docs/
└── overrides/
    └── partials/
        └── comments.html
```

### 第三步：创建 comments.html

在 `docs/overrides/partials/comments.html` 中创建文件：

```html
{% if page.meta.comments %}
  <h2 id="__comments">评论</h2>
  <script src="https://giscus.app/client.js"
          data-repo="你的用户名/你的仓库名"
          data-repo-id="你的仓库ID"
          data-category="你的分类名"
          data-category-id="你的分类ID"
          data-mapping="pathname"
          data-strict="0"
          data-reactions-enabled="1"
          data-emit-metadata="0"
          data-input-position="bottom"
          data-theme="preferred_color_scheme"
          data-lang="zh-CN"
          crossorigin="anonymous"
          async>
  </script>
  
  <!-- 同步 Giscus 主题与调色板 -->
  <script>
    var giscus = document.querySelector("script[src*=giscus]")

    // 初始加载时设置调色板
    var palette = __md_get("__palette")
    if (palette && typeof palette.color === "object") {
      var theme = palette.color.scheme === "slate"
        ? "transparent_dark"
        : "light"

      // 指示 Giscus 设置主题
      giscus.setAttribute("data-theme", theme) 
    }

    // 文档加载后注册事件处理器
    document.addEventListener("DOMContentLoaded", function() {
      var ref = document.querySelector("[data-md-component=palette]")
      ref.addEventListener("change", function() {
        var palette = __md_get("__palette")
        if (palette && typeof palette.color === "object") {
          var theme = palette.color.scheme === "slate"
            ? "transparent_dark"
            : "light"

          // 指示 Giscus 更改主题
          var frame = document.querySelector(".giscus-frame")
          if (frame) {
            frame.contentWindow.postMessage(
              { giscus: { setConfig: { theme } } },
              "https://giscus.app"
            )
          }
        }
      })
    })
  </script>
{% endif %}
```

### 第四步：获取 Giscus 配置

1. 访问 [Giscus 配置页面](https://giscus.app/zh-CN)
2. 填写你的 GitHub 仓库信息
3. 选择分类（或创建新分类）
4. 复制生成的配置代码
5. 替换 `comments.html` 中的配置项

### 第五步：在页面中启用评论

在需要显示评论的页面 front matter 中添加：

```markdown
---
title: 我的文章
comments: true
---

# 我的文章

文章内容...
```

## 其他评论系统

### Twikoo

Twikoo 是一个简洁、安全、免费的静态网站评论系统。

#### 配置步骤

1. 在 `docs/overrides/partials/comments.html` 中添加：

```html
{% if page.meta.comments %}
  <div id="tcomment"></div>
  <script src="https://cdn.staticfile.org/twikoo/1.6.21/twikoo.all.min.js"></script>
  <script>
    twikoo.init({
      envId: '你的环境ID',  // 腾讯云环境填 envId；Vercel 环境填地址
      el: '#tcomment',
      lang: 'zh-CN',
      path: location.pathname,
      onCommentLoaded: function () {
        console.log('评论加载完成');
      }
    })
  </script>
{% endif %}
```

2. 在页面 front matter 中启用：

```markdown
---
title: 我的文章
comments: true
---
```

### Valine

Valine 是一个快速、简洁且高效的评论系统。

```html
{% if page.meta.comments %}
  <div id="vcomments"></div>
  <script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
  <script src="//unpkg.com/valine/dist/Valine.min.js"></script>
  <script>
    new Valine({
      el: '#vcomments',
      appId: '你的AppID',
      appKey: '你的AppKey',
      placeholder: '请输入评论...',
      lang: 'zh-CN'
    })
  </script>
{% endif %}
```

## 即时导航兼容性

如果使用即时导航，需要监听 `document$` 事件：

```javascript
// 原方式（不适用于即时导航）
document.addEventListener('DOMContentLoaded', function() {
    // 初始化评论
});

// Zensical 即时导航兼容
document$.subscribe(function() {
    // 初始化评论
    if (window.giscus) {
        // 重新初始化 Giscus
    }
});
```

## 完整配置示例

### docs/overrides/partials/comments.html

```html
{% if page.meta.comments %}
  <h2 id="__comments">评论</h2>
  <script src="https://giscus.app/client.js"
          data-repo="Wcowin/Zensical-Chinese-Tutorial"
          data-repo-id="R_kgDO..."
          data-category="Announcements"
          data-category-id="DIC_kwDO..."
          data-mapping="pathname"
          data-strict="0"
          data-reactions-enabled="1"
          data-emit-metadata="0"
          data-input-position="bottom"
          data-theme="preferred_color_scheme"
          data-lang="zh-CN"
          crossorigin="anonymous"
          async>
  </script>
  
  <script>
    (function() {
      var giscus = document.querySelector("script[src*=giscus]")
      if (!giscus) return;

      function setTheme(theme) {
        var frame = document.querySelector(".giscus-frame");
        if (frame && frame.contentWindow) {
          frame.contentWindow.postMessage(
            { giscus: { setConfig: { theme } } },
            "https://giscus.app"
          );
        }
      }

      // 初始主题
      var palette = __md_get("__palette");
      if (palette && typeof palette.color === "object") {
        var theme = palette.color.scheme === "slate" ? "transparent_dark" : "light";
        giscus.setAttribute("data-theme", theme);
      }

      // 监听主题切换
      document.addEventListener("DOMContentLoaded", function() {
        var ref = document.querySelector("[data-md-component=palette]");
        if (ref) {
          ref.addEventListener("change", function() {
            var palette = __md_get("__palette");
            if (palette && typeof palette.color === "object") {
              var theme = palette.color.scheme === "slate" ? "transparent_dark" : "light";
              setTheme(theme);
            }
          });
        }
      });

      // 即时导航兼容
      if (typeof document$ !== "undefined") {
        document$.subscribe(function() {
          var palette = __md_get("__palette");
          if (palette && typeof palette.color === "object") {
            var theme = palette.color.scheme === "slate" ? "transparent_dark" : "light";
            setTheme(theme);
          }
        });
      }
    })();
  </script>
{% endif %}
```

## 常见问题

### 评论不显示

**问题**：配置后评论不显示

**解决方案**：
1. 检查 `comments: true` 是否在 front matter 中
2. 检查 Giscus 配置是否正确
3. 检查 GitHub Discussions 是否已启用
4. 查看浏览器控制台是否有错误

### 主题不同步

**问题**：评论系统主题与网站主题不一致

**解决方案**：
1. 确保主题同步脚本已正确添加
2. 检查调色板配置
3. 手动刷新页面

### 即时导航问题

**问题**：使用即时导航后评论不加载

**解决方案**：
1. 添加 `document$` 事件监听
2. 在页面切换时重新初始化评论系统

## 参考资源

- [Giscus 官方文档](https://giscus.app/zh-CN)
- [Twikoo 官方文档](https://twikoo.js.org/)
- [Valine 官方文档](https://valine.js.org/)
- [Zensical 模板覆盖](https://zensical.org/docs/)

---

**提示**：选择合适的评论系统可以增强用户互动！

