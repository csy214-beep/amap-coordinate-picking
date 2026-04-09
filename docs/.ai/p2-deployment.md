# 部署指南

## 概述

本文档说明项目的生产部署步骤。

---

## 构建生产版本

### 1. 执行构建

```bash
npm run build
# 或
pnpm build
```

### 2. 构建产物

构建完成后，输出目录为 `dist/`，包含：

```
dist/
├── index.html
├── assets/
│   ├── index-*.js
│   └── index-*.css
└── ...
```

---

## 部署前检查清单

- [ ] 配置正确的高德地图 API Key
- [ ] 在高德开放平台配置生产环境域名白名单
- [ ] 检查环境变量配置
- [ ] 执行构建并测试
- [ ] 确认 HTTPS 配置（推荐）

---

## 部署方式

### 静态文件托管

将 `dist/` 目录的内容部署到任意静态文件服务器：

- Nginx
- Apache
- GitHub Pages
- Vercel
- Netlify
- 阿里云 OSS / CDN
- 腾讯云 COS
- 等等

### Nginx 配置示例

```nginx
server {
  listen 80;
  server_name your-domain.com;

  root /path/to/dist;
  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }

  # Gzip 压缩
  gzip on;
  gzip_types text/plain text/css application/json application/javascript text/xml application/xml;
}
```

---

## 环境变量

生产环境需要配置：

| 变量 | 说明 |
|------|------|
| VITE_APP_API_KEY | 高德地图 API Key |
| VITE_APP_MAP_SECURITY | 安全密钥 |

**注意**: 环境变量在构建时被内联到代码中。

---

## 高德地图配置

### 域名白名单

在高德开放平台控制台：

1. 进入「应用管理」→「我的应用」
2. 找到对应的应用
3. 点击「设置」
4. 在「域名白名单」中添加生产域名

**示例**:
```
your-domain.com
www.your-domain.com
```

###  HTTPS

生产环境强烈建议使用 HTTPS，以确保安全性。

---

## 监控与维护

### 错误监控

建议添加前端错误监控：
- Sentry
- 阿里云 ARMS
- 腾讯云前端监控

### 性能监控

关注：
- 地图加载时间
- 首屏渲染时间
- 交互响应时间

---

## 回滚方案

如果部署出现问题：

1. 保留上一个版本的构建产物
2. 快速切换回上一版本
3. 检查问题并修复后重新部署

---

## 相关文档

- [开发环境配置](./p0-dev-setup.md)
- [配置文件说明](./p1-config-files.md)
