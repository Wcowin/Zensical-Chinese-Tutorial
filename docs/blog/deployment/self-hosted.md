---
title: 自托管部署
date: 2025-01-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 部署指南
---

# 自托管部署

> 在自己的服务器上部署 Zensical 网站

## 什么是自托管？

自托管是指在自己的服务器（VPS、云服务器等）上部署网站，拥有完全的控制权：

- ✅ **完全控制** - 自由配置服务器
- ✅ **无限制** - 没有流量和存储限制
- ✅ **高性能** - 可以优化服务器性能
- ✅ **隐私保护** - 数据完全在自己掌控中

## 准备工作

在开始之前，你需要：

- [x] 一台 Linux 服务器（Ubuntu/Debian/CentOS）
- [x] 服务器的 SSH 访问权限
- [x] 域名（可选，但推荐）
- [x] 基本的 Linux 命令知识

## 方法一：使用 Nginx 部署（推荐）

### 第一步：构建网站

在本地构建网站：

```bash
zensical build
```

这会在 `site/` 目录生成静态文件。

### 第二步：上传文件到服务器

使用 `scp` 或 `rsync` 上传文件：

```bash
# 使用 scp
scp -r site/* user@your-server:/var/www/your-site/

# 使用 rsync（推荐，支持增量同步）
rsync -avz --delete site/ user@your-server:/var/www/your-site/
```

### 第三步：安装 Nginx

在服务器上安装 Nginx：

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install nginx

# CentOS/RHEL
sudo yum install nginx
```

### 第四步：配置 Nginx

创建 Nginx 配置文件 `/etc/nginx/sites-available/your-site`：

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name example.com www.example.com;

    root /var/www/your-site;
    index index.html;

    # 启用 gzip 压缩
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_types text/plain text/css text/xml text/javascript 
               application/x-javascript application/xml+rss 
               application/json application/javascript;

    # 主要位置配置
    location / {
        try_files $uri $uri/ =404;
    }

    # 缓存静态资源
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2|ttf|eot)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # 404 页面
    error_page 404 /404.html;
    location = /404.html {
        internal;
    }

    # 安全头
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
}
```

### 第五步：启用站点

```bash
# 创建符号链接
sudo ln -s /etc/nginx/sites-available/your-site /etc/nginx/sites-enabled/

# 测试配置
sudo nginx -t

# 重启 Nginx
sudo systemctl restart nginx
```

### 第六步：配置 HTTPS（使用 Let's Encrypt）

安装 Certbot：

```bash
# Ubuntu/Debian
sudo apt install certbot python3-certbot-nginx

# CentOS/RHEL
sudo yum install certbot python3-certbot-nginx
```

获取 SSL 证书：

```bash
sudo certbot --nginx -d example.com -d www.example.com
```

Certbot 会自动配置 HTTPS 并设置自动续期。

## 方法二：使用 Apache 部署

### 安装 Apache

```bash
# Ubuntu/Debian
sudo apt install apache2

# CentOS/RHEL
sudo yum install httpd
```

### 配置 Apache

创建配置文件 `/etc/apache2/sites-available/your-site.conf`：

```apache
<VirtualHost *:80>
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/your-site

    <Directory /var/www/your-site>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    # 启用压缩
    <IfModule mod_deflate.c>
        AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript
    </IfModule>

    # 缓存控制
    <IfModule mod_expires.c>
        ExpiresActive On
        ExpiresByType image/jpg "access plus 1 year"
        ExpiresByType image/jpeg "access plus 1 year"
        ExpiresByType image/gif "access plus 1 year"
        ExpiresByType image/png "access plus 1 year"
        ExpiresByType text/css "access plus 1 year"
        ExpiresByType application/javascript "access plus 1 year"
    </IfModule>

    ErrorLog ${APACHE_LOG_DIR}/your-site-error.log
    CustomLog ${APACHE_LOG_DIR}/your-site-access.log combined
</VirtualHost>
```

### 启用站点

```bash
# 启用站点
sudo a2ensite your-site

# 启用必要的模块
sudo a2enmod rewrite deflate expires

# 重启 Apache
sudo systemctl restart apache2
```

## 方法三：使用 Docker 部署

### 创建 Dockerfile

```dockerfile
FROM nginx:alpine

# 复制构建文件
COPY site/ /usr/share/nginx/html/

# 复制 Nginx 配置
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### 创建 nginx.conf

```nginx
server {
    listen 80;
    server_name localhost;
    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;
}
```

### 构建和运行

```bash
# 构建镜像
docker build -t my-zensical-site .

# 运行容器
docker run -d -p 80:80 --name my-site my-zensical-site
```

### 使用 docker-compose

创建 `docker-compose.yml`：

```yaml
version: '3'

services:
  web:
    build: .
    ports:
      - "80:80"
    restart: unless-stopped
```

运行：

```bash
docker-compose up -d
```

## 自动化部署

### 使用 Git Hooks

在服务器上设置 Git 仓库：

```bash
# 创建裸仓库
mkdir -p /var/repo/your-site.git
cd /var/repo/your-site.git
git init --bare

# 创建 post-receive hook
cat > hooks/post-receive << 'EOF'
#!/bin/bash
GIT_WORK_TREE=/var/www/your-site git checkout -f
cd /var/www/your-site
zensical build
EOF

chmod +x hooks/post-receive
```

在本地添加远程仓库：

```bash
git remote add production user@your-server:/var/repo/your-site.git
```

部署：

```bash
git push production main
```

### 使用 GitHub Actions

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to Server

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install Zensical
        run: pip install zensical

      - name: Build
        run: zensical build

      - name: Deploy to Server
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          source: "site/*"
          target: "/var/www/your-site/"
          strip_components: 1
```

## 性能优化

### 启用 HTTP/2

在 Nginx 配置中：

```nginx
listen 443 ssl http2;
listen [::]:443 ssl http2;
```

### 配置缓存

```nginx
# 浏览器缓存
location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

# Nginx 缓存
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m;
```

### 启用 Brotli 压缩

```bash
# 安装 Brotli 模块
sudo apt install nginx-module-brotli

# 在 Nginx 配置中启用
brotli on;
brotli_types text/plain text/css application/json application/javascript text/xml application/xml;
```

## 安全配置

### 配置防火墙

```bash
# UFW (Ubuntu)
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable

# Firewalld (CentOS)
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

### 配置 SSL 安全性

在 Nginx 配置中添加：

```nginx
# SSL 配置
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers HIGH:!aNULL:!MD5;
ssl_prefer_server_ciphers on;

# HSTS
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

# 其他安全头
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
```

## 监控和维护

### 日志管理

```bash
# 查看访问日志
sudo tail -f /var/log/nginx/access.log

# 查看错误日志
sudo tail -f /var/log/nginx/error.log

# 日志轮转
sudo logrotate -f /etc/logrotate.d/nginx
```

### 性能监控

使用工具如：
- **htop** - 系统资源监控
- **nginx-amplify** - Nginx 性能监控
- **Prometheus + Grafana** - 全面监控方案

## 常见问题

### 权限问题

```bash
# 设置正确的权限
sudo chown -R www-data:www-data /var/www/your-site
sudo chmod -R 755 /var/www/your-site
```

### 404 错误

检查：
1. 文件路径是否正确
2. Nginx 配置中的 `root` 路径
3. `index.html` 是否存在

### SSL 证书问题

```bash
# 测试证书续期
sudo certbot renew --dry-run

# 手动续期
sudo certbot renew
```

## 完整配置示例

### Nginx 完整配置（带 HTTPS）

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name example.com www.example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name example.com www.example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    root /var/www/your-site;
    index index.html;

    gzip on;
    gzip_vary on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    error_page 404 /404.html;

    add_header Strict-Transport-Security "max-age=31536000" always;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
}
```


**参考资料**：  

- [Nginx 官方文档](https://nginx.org/en/docs/)  
- [Let's Encrypt 文档](https://letsencrypt.org/docs/)  
- [Docker 官方文档](https://docs.docker.com/)
