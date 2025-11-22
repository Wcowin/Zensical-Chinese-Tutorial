---
title: 自定义网站字体
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 高级主题
---

# 自定义网站字体

> 为你的 Zensical 网站添加美观的中文字体

## 概述

Zensical 支持自定义字体，你可以使用各种中文字体来美化你的网站。本文以**霞鹜文楷**为例，介绍如何配置自定义字体。

## 推荐字体

### 霞鹜文楷（LXGW WenKai）

霞鹜文楷是一款开源中文字体，基于 FONTWORKS 的 Klee One 衍生，具有文艺气息，适合阅读。

- **开源免费**：SIL Open Font License 1.1
- **美观优雅**：适合正文阅读
- **多版本**：完整版、轻便版、屏幕版等

更多信息：[霞鹜文楷 GitHub](https://github.com/lxgw/LxgwWenKai)

## 配置方法

### 第一步：添加字体 CSS

在 `zensical.toml` 中添加字体 CSS：

```toml
extra_css = [
    "stylesheets/extra.css",
    "https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.1.0/style.css",  # 霞鹜文楷
]
```

### 第二步：配置字体样式

在 `docs/stylesheets/extra.css` 中添加：

```css
@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.1.0/style.css');

body {
    font-family: "LXGW WenKai", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    font-weight: normal;
}

/* 返回顶部按钮字体 */
button.md-top {
    font-family: "LXGW WenKai";
    font-size: 16px;
    font-weight: bold;
}
```

### 第三步：使用其他字体源

你也可以使用其他字体 CDN：

```css
/* 使用 zeoseven 字体服务 */
@import url('https://fontsapi.zeoseven.com/292/main/result.css');

body {
    font-family: "LXGW WenKai";
}
```

## 其他推荐字体

### 1. 霞鹜文楷屏幕版

适合屏幕阅读，字重更粗：

```css
@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-screen-webfont@1.1.0/style.css');

body {
    font-family: "LXGW WenKai Screen";
}
```

### 2. 霞鹜文楷轻便版

体积更小，适合嵌入：

```css
@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-lite-webfont@1.1.0/style.css');

body {
    font-family: "LXGW WenKai Lite";
}
```

### 3. 汇文明朝体

```css
@import url('https://chinese-fonts-cdn.deno.dev/packages/hwmct/dist/%E6%B1%87%E6%96%87%E6%98%8E%E6%9C%9D%E4%BD%93/result.css');

body {
    font-family: "Huiwen-mincho";
}
```

## 字体配置选项

### 在 zensical.toml 中配置

```toml
[project.theme.font]
text = "LXGW WenKai"  # 文本字体
code = "Roboto Mono"  # 代码字体
```

### 使用 CSS 变量

```css
:root {
    --md-text-font: "LXGW WenKai";
    --md-code-font: "Roboto Mono";
}
```

## 完整配置示例

### zensical.toml

```toml
[project.theme]
custom_dir = "docs/overrides"

extra_css = [
    "stylesheets/extra.css",
    "https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.1.0/style.css",
]
```

### stylesheets/extra.css

```css
@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.1.0/style.css');

body {
    font-family: "LXGW WenKai", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    font-weight: normal;
}

/* 代码块字体保持不变 */
code, pre {
    font-family: "Roboto Mono", "Consolas", monospace;
}

/* 返回顶部按钮 */
button.md-top {
    font-family: "LXGW WenKai";
    font-size: 16px;
    font-weight: bold;
}
```

## 注意事项

1. **字体加载**：使用 CDN 字体时，注意加载速度
2. **备用字体**：建议设置备用字体，防止加载失败
3. **性能影响**：字体文件较大时可能影响页面加载速度
4. **浏览器兼容**：确保字体格式兼容目标浏览器

## 字体资源

- [霞鹜文楷 GitHub](https://github.com/lxgw/LxgwWenKai)
- [中文字体 CDN](https://chinese-font.netlify.app/)
- [zeoseven 字体服务](https://fonts.zeoseven.com/)
- [jsDelivr CDN](https://www.jsdelivr.com/)

## 常见问题

### 字体不生效

**问题**：配置后字体没有变化

**解决方案**：
1. 检查 CSS 文件路径是否正确
2. 清除浏览器缓存
3. 检查字体名称是否正确
4. 查看浏览器控制台是否有错误

### 字体加载慢

**问题**：字体加载时间过长

**解决方案**：
1. 使用本地字体文件
2. 使用字体子集
3. 使用字体预加载
4. 考虑使用轻便版字体

### 代码块字体异常

**问题**：代码块也使用了中文字体

**解决方案**：
```css
code, pre {
    font-family: "Roboto Mono", "Consolas", monospace !important;
}
```

---

**提示**：选择合适的字体可以大大提升网站的阅读体验！

