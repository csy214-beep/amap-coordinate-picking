# 项目架构总览

## 项目概览

**amap-coordinate-picking** 是一个基于 Vue 3 + TypeScript + Vite 构建的高德地图坐标拾取工具。

### 技术栈

| 类别 | 技术 | 版本 |
|------|------|------|
| 前端框架 | Vue 3 | ^3.5.17 |
| 开发语言 | TypeScript | ~5.8.3 |
| 构建工具 | Vite | ^7.0.4 |
| 地图 API | 高德地图 JS API 2.x | - |

## 目录结构

```
amap-coordinate-picking/
├── public/                    # 静态资源
│   └── vite.svg
├── src/
│   ├── assets/
│   │   └── map-styles.css    # 地图样式
│   ├── components/            # Vue 组件
│   │   ├── MapDrawer.vue      # 核心地图绘制组件
│   │   ├── AddressSearch.vue  # 地址搜索组件
│   │   └── MapError.vue       # 错误提示组件
│   ├── config/
│   │   └── mapConfig.ts       # 地图配置
│   ├── types/
│   │   └── map.ts             # TypeScript 类型定义
│   ├── App.vue                # 根组件
│   ├── main.ts                # 应用入口
│   └── vite-env.d.ts
├── index.html
├── package.json
├── tsconfig*.json
└── vite.config.ts
```

## 核心组件关系

### 1. App.vue (根组件)
- 负责检查高德地图 API 加载状态
- 根据加载状态显示：MapDrawer / MapError / 加载动画

### 2. MapDrawer.vue (核心组件)
- 地图初始化与管理
- 绘制模式切换
- 图形绘制（多边形、矩形、圆形）
- 点击获取坐标
- 数据导出
- **最新功能**：点击模式撤销操作

### 3. AddressSearch.vue (地址搜索)
- 地址输入与搜索
- POI 搜索结果展示
- 位置选择与定位

## 数据流

### 地图绘制流程

```
用户选择绘制模式
    ↓
点击地图获取坐标点
    ↓
更新临时图形/标记
    ↓
完成绘制 → 添加到 drawnShapes 数组
    ↓
获取坐标 / 导出数据
```

### 点击模式流程（含撤销）

```
进入点击模式
    ↓
点击地图添加点 → clickPoints 数组
    ↓
（可选）Ctrl+Z 或点击按钮撤销
    ↓
    ├─→ undoLastClickPoint()
    │      ├─ pop clickPoints
    │      └─ 移除地图标记
    ↓
清除 / 导出数据
```

## 关键数据结构

详见 [类型定义文档](./p1-types-definition.md)

| 类型 | 说明 |
|------|------|
| Coordinate | 坐标点 {lng, lat} |
| DrawMode | 绘制模式 |
| ShapeData | 图形数据 |
| DrawnShape | 绘制的图形对象 |

## 配置管理

所有配置集中在 `src/config/mapConfig.ts`，通过环境变量注入：
- VITE_APP_API_KEY: 高德地图 API Key
- VITE_APP_MAP_SECURITY: 安全密钥

## 下一步

- 了解核心组件：[MapDrawer 组件详解](./p0-map-drawer.md)
- 配置开发环境：[开发环境配置](./p0-dev-setup.md)
