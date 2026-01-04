---
title: 性能优化
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 高级主题
---

# 性能优化

> 优化你的 Zensical 网站性能

!!! info "Zensical 性能优势"
    Zensical 使用 Rust 构建的高性能运行时 (ZRX)，相比 MkDocs 有显著的性能提升。官方正在持续优化构建性能和缓存机制。

## Zensical 内置优化

### Rust 运行时

Zensical 的核心优势之一是其 Rust 运行时：

- ✅ **并行渲染** - 模板可以并行渲染
- ✅ **智能缓存** - 自动缓存中间结果
- ✅ **高效 I/O** - 优化的文件读写
- ✅ **内存效率** - 更低的内存占用

### 即时导航

启用即时导航可以大幅提升用户体验：

```toml
[project.theme]
features = [
    "navigation.instant",           # 即时导航
    "navigation.instant.prefetch",  # 预加载链接
]
```

**效果：**

- 页面切换无需完整刷新
- 预加载减少等待时间
- 类似单页应用的体验

## 构建优化

### 清理构建

定期清理构建缓存：

```bash
zensical build --clean
```

### 增量构建

开发时使用增量构建：

```bash
zensical build --dirty
```

!!! warning "关于缓存"
    官方目前不推荐在 CI 系统中使用缓存，因为缓存功能正在优化中。

## 内容优化

### 图片优化

#### 使用合适的格式

| 格式 | 适用场景 | 特点 |
|------|----------|------|
| WebP | 通用图片 | 体积小，兼容性好 |
| AVIF | 现代浏览器 | 体积最小 |
| SVG | 图标、图表 | 矢量，无限缩放 |
| PNG | 需要透明 | 无损压缩 |
| JPEG | 照片 | 有损压缩 |

#### 图片压缩工具

- **TinyPNG** - 在线压缩 PNG/JPEG
- **Squoosh** - Google 开源图片压缩
- **ImageOptim** - macOS 图片优化
- **Sharp** - Node.js 图片处理库

#### 响应式图片

```markdown
![图片](image.png){: loading="lazy" width="800" }
```

### 懒加载

为图片启用懒加载：

```html
<img src="image.png" loading="lazy" alt="描述">
```

或在 Markdown 中：

```markdown
![描述](image.png){: loading="lazy" }
```

### 减少外部资源

尽量减少外部 CSS/JS：

```toml
# 只加载必要的资源
extra_css = [
    "stylesheets/extra.css",  # 本地样式
]

extra_javascript = [
    "javascripts/extra.js",   # 本地脚本
]
```

## 主题优化

### 禁用不需要的功能

只启用需要的功能：

```toml
[project.theme]
features = [
    # 只启用必要的功能
    "navigation.instant",
    "navigation.top",
    "search.suggest",
    "content.code.copy",
]
```

### 优化调色板

减少调色板数量：

```toml
# 只使用一个调色板（如果不需要明暗切换）
[[project.theme.palette]]
scheme = "default"
primary = "indigo"
accent = "indigo"
```

## 部署优化

### 启用 Gzip/Brotli 压缩

#### Nginx 配置

```nginx
# Gzip 压缩
gzip on;
gzip_vary on;
gzip_min_length 1024;
gzip_types text/plain text/css text/xml text/javascript 
           application/javascript application/json 
           application/xml+rss;

# Brotli 压缩（如果支持）
brotli on;
brotli_types text/plain text/css application/json 
             application/javascript text/xml application/xml;
```

### 配置缓存策略

```nginx
# 静态资源长期缓存
location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

# HTML 短期缓存
location ~* \.html$ {
    expires 1h;
    add_header Cache-Control "public, must-revalidate";
}
```

### 使用 CDN

推荐的 CDN 服务：

- **Cloudflare** - 免费 CDN，全球节点
- **Vercel Edge** - 边缘网络
- **AWS CloudFront** - AWS CDN
- **Fastly** - 高性能 CDN

## 性能测试

### 测试工具

- **Lighthouse** - Chrome 内置性能测试
- **PageSpeed Insights** - Google 页面速度分析
- **WebPageTest** - 详细性能分析
- **GTmetrix** - 综合性能报告

### 关键指标

| 指标 | 目标值 | 说明 |
|------|--------|------|
| FCP | < 1.8s | 首次内容绘制 |
| LCP | < 2.5s | 最大内容绘制 |
| CLS | < 0.1 | 累积布局偏移 |
| TTI | < 3.8s | 可交互时间 |

### 本地性能测试

```bash
# 使用 Lighthouse CLI
npm install -g lighthouse
lighthouse https://your-site.com --view

# 构建时间测试
time zensical build --clean
```

## 最佳实践清单

### 内容层面

- [ ] 压缩所有图片
- [ ] 使用 WebP/AVIF 格式
- [ ] 启用图片懒加载
- [ ] 减少页面大小

### 配置层面

- [ ] 启用即时导航
- [ ] 只启用必要功能
- [ ] 优化 Markdown 扩展配置

### 部署层面

- [ ] 启用 Gzip/Brotli 压缩
- [ ] 配置合理的缓存策略
- [ ] 使用 CDN 加速
- [ ] 启用 HTTPS

## 常见问题

### 构建时间过长

**解决方案：**

1. 减少不必要的插件
2. 优化图片大小
3. 使用增量构建
4. 等待官方缓存优化

### 页面加载慢

**解决方案：**

1. 启用即时导航
2. 压缩静态资源
3. 使用 CDN
4. 检查外部资源加载

## 参考资源

- [Zensical Roadmap](https://zensical.org/about/roadmap/)
- [Web Vitals](https://web.dev/vitals/)
- [Lighthouse 文档](https://developer.chrome.com/docs/lighthouse/)

---

**提示**：Zensical 的 Rust 运行时已经提供了出色的性能，大多数情况下无需额外优化！
