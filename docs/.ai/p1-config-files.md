# 配置文件说明

## 概述

本文档说明项目中的主要配置文件。

---

## src/config/mapConfig.ts

**文件路径**: `src/config/mapConfig.ts`

这是高德地图的核心配置文件。

### 配置项

```typescript
export const MAP_CONFIG: MapConfig = {
  API_KEY: import.meta.env.VITE_APP_API_KEY,
  securityJsCode: import.meta.env.VITE_APP_MAP_SECURITY,
  MAP_OPTIONS: {
    zoom: 13,
    center: [116.397428, 39.90923],  // 北京天安门
    mapStyle: "amap://styles/normal",
  },
  DRAW_STYLES: { ... },
  CIRCLE_SEGMENTS: 32,
  MARKER_SIZE: 10,
};
```

### MAP_OPTIONS

| 字段 | 说明 |
|------|------|
| zoom | 地图初始缩放级别 |
| center | 地图中心点坐标 [经度, 纬度] |
| mapStyle | 地图样式 |

### DRAW_STYLES

图形绘制样式配置。

#### polygon (多边形)

| 字段 | 说明 |
|------|------|
| strokeColor | 边框颜色 |
| strokeWeight | 边框粗细 |
| fillColor | 填充颜色 |
| fillOpacity | 填充透明度 |

#### rectangle (矩形)

同 polygon 配置。

#### circle (圆形)

同 polygon 配置。

#### temp (临时图形)

| 字段 | 说明 |
|------|------|
| strokeStyle | 边框样式 ('dashed' 虚线) |
| fillOpacity | 填充透明度 |

### 其他配置

| 字段 | 说明 |
|------|------|
| CIRCLE_SEGMENTS | 圆形近似的点数（越多越圆） |
| MARKER_SIZE | 临时标记点大小 |

---

## .env / .env.example

**文件路径**: `.env` (需自行创建)

环境变量配置文件。

```env
VITE_APP_API_KEY=your-api-key-here
VITE_APP_MAP_SECURITY=your-security-code-here
```

### 变量说明

| 变量名 | 说明 |
|--------|------|
| VITE_APP_API_KEY | 高德地图 API Key |
| VITE_APP_MAP_SECURITY | 高德地图安全密钥 |

### 注意事项

- `.env` 文件已在 `.gitignore` 中，不要提交到版本控制
- 复制 `.env.example` 为 `.env` 并填入实际值

---

## package.json

**文件路径**: `package.json`

项目依赖和脚本配置。

### Scripts

| 命令 | 说明 |
|------|------|
| `npm run dev` | 启动开发服务器 |
| `npm run build` | 构建生产版本 |
| `npm run preview` | 预览构建结果 |

### Dependencies

| 包名 | 说明 |
|------|------|
| vue | Vue 3 框架 |

### DevDependencies

| 包名 | 说明 |
|------|------|
| @types/amap-js-api | 高德地图类型定义 |
| @vitejs/plugin-vue | Vite Vue 插件 |
| typescript | TypeScript |
| vite | 构建工具 |
| vue-tsc | Vue TypeScript 编译器 |

---

## vite.config.ts

**文件路径**: `vite.config.ts`

Vite 构建工具配置。

---

## tsconfig*.json

TypeScript 配置文件:
- `tsconfig.json` - 基础配置
- `tsconfig.app.json` - 应用配置
- `tsconfig.node.json` - Node 环境配置

---

## 相关文档

- [开发环境配置](./p0-dev-setup.md)
- [类型定义文档](./p1-types-definition.md)
