---
title: SEO 优化
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 高级主题
---

# SEO 优化

> 提升你的 Zensical 网站在搜索引擎中的排名

## 基础 SEO 配置

### 必要的元数据

在 `zensical.toml` 中配置基础 SEO 信息：

```toml
[project]
site_name = "我的网站"
site_url = "https://example.com"           # 必须设置！
site_description = "网站描述，50-160 字符"
site_author = "作者名称"
```

!!! warning "site_url 很重要"
    `site_url` 是 SEO 的基础，影响：
    
    - 规范链接 (canonical URL)
    - 站点地图 (sitemap)
    - 社交分享链接
    - RSS 订阅链接

### 页面元数据

在每个页面的 front matter 中添加：

```markdown
---
title: 页面标题 - 简洁有吸引力
description: 页面描述，50-160 字符，包含关键词
---
```

## 结构化数据

### 标题层级

正确使用标题层级：

```markdown
# H1 - 页面主标题（每页只有一个）

## H2 - 主要章节

### H3 - 子章节

#### H4 - 更细分的内容
```

!!! tip "标题最佳实践"
    - 每页只有一个 H1
    - 标题层级不要跳跃（H1 → H3）
    - 标题包含关键词
    - 标题简洁明了

### 内部链接

建立良好的内部链接结构：

```markdown
相关内容请参考 [配置详解](../tutorials/configuration.md)。

更多信息请查看：

- [快速开始](../getting-started/quick-start.md)
- [主题定制](../tutorials/theme-customization.md)
```

## 技术 SEO

### 站点地图

Zensical 自动生成 `sitemap.xml`，确保：

1. 站点地图可访问：`https://your-site.com/sitemap.xml`
2. 提交到 Google Search Console
3. 提交到 Bing Webmaster Tools

### robots.txt

在 `docs/` 目录创建 `robots.txt`：

```
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```

### 规范链接

Zensical 自动添加规范链接，确保 `site_url` 配置正确。

## 内容 SEO

### 关键词优化

#### 标题优化

```markdown
---
title: Python 装饰器完全指南 - 从入门到精通
description: 学习 Python 装饰器的完整教程，包含基础概念、实际案例和最佳实践。
---
```

#### 内容优化

- 在前 100 字包含主要关键词
- 自然地使用相关关键词
- 使用同义词和相关术语
- 避免关键词堆砌

### 内容质量

搜索引擎偏好：

- ✅ **原创内容** - 独特有价值的内容
- ✅ **深度内容** - 全面详细的解释
- ✅ **更新频率** - 定期更新内容
- ✅ **用户体验** - 易读、结构清晰

### 图片 SEO

```markdown
![Python 装饰器工作原理示意图](decorator-diagram.png)
```

**最佳实践：**

- 使用描述性文件名：`python-decorator-diagram.png`
- 添加有意义的 alt 文本
- 压缩图片大小
- 使用 WebP 格式

## 社交媒体优化

### Open Graph 标签

在页面 front matter 中添加：

```markdown
---
title: 页面标题
description: 页面描述
image: assets/og-image.png
---
```

### 社交分享图片

创建吸引人的分享图片：

- 尺寸：1200 x 630 像素
- 包含标题和品牌元素
- 清晰易读

## 性能与 SEO

### Core Web Vitals

Google 将页面体验作为排名因素：

| 指标 | 目标 | 说明 |
|------|------|------|
| LCP | < 2.5s | 最大内容绘制 |
| FID | < 100ms | 首次输入延迟 |
| CLS | < 0.1 | 累积布局偏移 |

### 移动端优化

Zensical 默认响应式设计，确保：

- 移动端可正常访问
- 文字大小适合阅读
- 按钮易于点击
- 无水平滚动

## SEO 工具

### Google 工具

- **Google Search Console** - 监控搜索表现
- **Google Analytics** - 流量分析
- **PageSpeed Insights** - 性能分析
- **Mobile-Friendly Test** - 移动端测试

### 其他工具

- **Bing Webmaster Tools** - Bing 搜索优化
- **Ahrefs** - 关键词和反向链接分析
- **Screaming Frog** - 网站爬虫分析
- **Yoast SEO** - SEO 检查清单

## SEO 检查清单

### 技术层面

- [ ] 设置正确的 `site_url`
- [ ] 生成并提交 sitemap
- [ ] 创建 robots.txt
- [ ] 启用 HTTPS
- [ ] 优化页面加载速度
- [ ] 确保移动端友好

### 内容层面

- [ ] 每页有唯一的 title 和 description
- [ ] 正确使用标题层级
- [ ] 图片有 alt 文本
- [ ] 建立内部链接
- [ ] 内容原创且有价值

### 监控层面

- [ ] 注册 Google Search Console
- [ ] 设置 Google Analytics
- [ ] 定期检查索引状态
- [ ] 监控关键词排名

## 常见问题

### 页面没有被索引

**解决方案：**

1. 检查 robots.txt 是否阻止爬虫
2. 提交 sitemap 到 Search Console
3. 手动请求索引
4. 检查页面是否有 noindex 标签

### 排名下降

**解决方案：**

1. 检查是否有技术问题
2. 分析竞争对手内容
3. 更新和改进内容
4. 检查反向链接变化

### 重复内容

**解决方案：**

1. 使用规范链接
2. 合并相似页面
3. 使用 301 重定向

## 参考资源

- [Google SEO 入门指南](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)
- [Google Search Console 帮助](https://support.google.com/webmasters)
- [Web Vitals](https://web.dev/vitals/)
- [Schema.org](https://schema.org/)

---

**提示**：SEO 是长期工作，持续优化内容质量是最重要的！
