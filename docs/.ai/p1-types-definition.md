# 类型定义文档

## 概述

TypeScript 类型定义位于 `src/types/map.ts`，定义了项目中所有与地图相关的类型。

---

## MapConfig 接口

地图配置接口。

```typescript
interface MapConfig {
  API_KEY: string;
  securityJsCode: string;
  MAP_OPTIONS: {
    zoom: number;
    center: [number, number];
    mapStyle: string;
  };
  DRAW_STYLES: {
    polygon: {
      strokeColor: string;
      strokeWeight: number;
      fillColor: string;
      fillOpacity: number;
    };
    rectangle: { ... };
    circle: { ... };
    temp: {
      strokeStyle: string;
      fillOpacity: number;
    };
  };
  CIRCLE_SEGMENTS: number;
  MARKER_SIZE: number;
}
```

**字段说明**:
- `API_KEY`: 高德地图 API 密钥
- `securityJsCode`: 安全密钥
- `MAP_OPTIONS`: 地图初始化选项
- `DRAW_STYLES`: 图形绘制样式配置
- `CIRCLE_SEGMENTS`: 圆形绘制的近似点数（默认 32）
- `MARKER_SIZE`: 标记点大小

---

## Coordinate 接口

坐标点接口。

```typescript
interface Coordinate {
  lng: number;  // 经度
  lat: number;  // 纬度
}
```

---

## DrawMode 类型

绘制模式类型。

```typescript
type DrawMode = 'polygon' | 'rectangle' | 'circle' | null;
```

**可选值**:
- `'polygon'`: 多边形
- `'rectangle'`: 矩形
- `'circle'`: 圆形
- `null`: 无绘制模式

---

## ShapeData 接口

图形数据接口。

```typescript
interface ShapeData {
  type: string;           // 图形类型
  points: any[];          // AMap.LngLat[] 类型的原始点
  coordinates: Coordinate[];  // 转换后的坐标数组
}
```

---

## DrawnShape 接口

绘制图形对象接口。

```typescript
interface DrawnShape {
  shape: any;  // AMap.Polygon | AMap.Rectangle | AMap.Circle
  data: ShapeData;  // 图形数据
}
```

---

## ExportData 接口

导出数据接口。

```typescript
interface ExportData {
  timestamp: string;
  type: string;
  shapes?: ShapeData[];
  points?: {
    index: number;
    longitude: number;
    latitude: number;
    coordinates: [number, number];
  }[];
}
```

**字段说明**:
- `timestamp`: ISO 格式时间戳
- `type`: 数据类型 (`'click_points'` 或 `'drawn_shapes'`)
- `shapes`: 绘制图形数组（可选）
- `points`: 点击点数组（可选）

---

## 使用示例

```typescript
import type { 
  Coordinate, 
  DrawMode, 
  ShapeData, 
  DrawnShape 
} from '../types/map';

const point: Coordinate = { lng: 116.397, lat: 39.909 };
const mode: DrawMode = 'polygon';

const shapeData: ShapeData = {
  type: 'polygon',
  points: [],
  coordinates: [point]
};
```

---

## 相关文档

- [项目架构总览](./p0-architecture-overview.md)
- [配置文件说明](./p1-config-files.md)
