# 第三方依赖说明

## 概述

本文档说明项目使用的第三方依赖库。

---

## 核心依赖

### Vue 3

**包名**: `vue`

**版本**: ^3.5.17

**用途**: 前端框架，提供响应式数据绑定和组件化开发能力。

**使用场景**: 整个应用的基础框架。

---

## 开发依赖

### TypeScript

**包名**: `typescript`

**版本**: ~5.8.3

**用途**: 类型安全的 JavaScript 超集。

**使用场景**: 整个项目的开发语言。

---

### Vite

**包名**: `vite`

**版本**: ^7.0.4

**用途**: 下一代前端构建工具，提供极速的开发体验。

**使用场景**: 项目构建和开发服务器。

---

### @vitejs/plugin-vue

**包名**: `@vitejs/plugin-vue`

**版本**: ^6.0.0

**用途**: Vite 的 Vue 3 单文件组件支持插件。

---

### vue-tsc

**包名**: `vue-tsc`

**版本**: ^2.2.12

**用途**: Vue 3 的 TypeScript 类型检查工具。

---

### @types/amap-js-api

**包名**: `@types/amap-js-api`

**版本**: ^1.4.11

**用途**: 高德地图 JavaScript API 的 TypeScript 类型定义。

**重要提示**: 项目中实际使用 `window.AMap` 访问全局对象，此包提供类型支持。

---

### @vue/tsconfig

**包名**: `@vue/tsconfig`

**版本**: ^0.7.0

**用途**: Vue 官方推荐的 TypeScript 配置预设。

---

## 外部服务

### 高德地图 API

**服务地址**: https://lbs.amap.com/

**用途**: 地图渲染、地理编码、地点搜索等功能。

**使用方式**: 通过 index.html 中的 script 标签加载。

**需要配置**:
- API Key
- 安全密钥 (securityJsCode)
- 域名白名单

---

## 相关文档

- [配置文件说明](./p1-config-files.md)
- [开发环境配置](./p0-dev-setup.md)
