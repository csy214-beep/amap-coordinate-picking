# MapDrawer 组件详解

## 概述

`MapDrawer.vue` 是项目的核心组件，负责地图初始化、图形绘制、坐标获取等所有核心功能。

**文件位置**: `src/components/MapDrawer.vue`

---

## 状态变量 (State)

| 变量名          | 类型                    | 说明                     |
| --------------- | ----------------------- | ------------------------ |
| map             | ref&lt;any&gt;          | 高德地图实例             |
| currentDrawMode | ref&lt;DrawMode&gt;     | 当前绘制模式             |
| drawnShapes     | ref&lt;DrawnShape[]&gt; | 已完成绘制的图形列表     |
| tempPoints      | ref&lt;any[]&gt;        | 临时点（绘制中）         |
| tempShape       | ref&lt;any&gt;          | 临时图形对象             |
| tempMarkers     | ref&lt;any[]&gt;        | 临时标记                 |
| clickMode       | ref&lt;boolean&gt;      | 是否处于点击获取坐标模式 |
| clickPoints     | ref&lt;any[]&gt;        | 点击获取的坐标列表       |
| clickMarkers    | ref&lt;any[]&gt;        | 点击点的标记             |

---

## 核心功能模块

### 1. 地图初始化 (initMap)

```typescript
const initMap = () => {
  map.value = new window.AMap.Map("map", {
    zoom: MAP_CONFIG.MAP_OPTIONS.zoom,
    center: MAP_CONFIG.MAP_OPTIONS.center,
    mapStyle: MAP_CONFIG.MAP_OPTIONS.mapStyle,
  });
  // 加载地图控件
  // 绑定点击事件
};
```

**关键步骤**:

- 初始化地图实例
- 加载 ToolBar、Scale、ControlBar 控件
- 绑定地图点击事件处理函数

---

### 2. 绘制模式管理

#### setDrawMode - 设置绘制模式

```typescript
const setDrawMode = (mode: DrawMode) => {
  clickMode.value = false;
  clearTempShape();
  tempPoints.value = [];
  currentDrawMode.value = mode;
};
```

#### toggleClickMode - 切换点击模式

```typescript
const toggleClickMode = () => {
  clickMode.value = !clickMode.value;
  if (clickMode.value) {
    clearDrawMode(); // 退出绘制模式
  }
};
```

---

### 3. 图形绘制功能

#### drawPolygon - 绘制多边形

| 阶段      | 说明               |
| --------- | ------------------ |
| 第 1 个点 | 创建 Polygon 实例  |
| 后续点    | 更新路径           |
| 完成      | 点击"完成绘制"按钮 |

#### drawRectangle - 绘制矩形

| 点        | 说明                |
| --------- | ------------------- |
| 第 1 个点 | 创建 Rectangle 实例 |
| 第 2 个点 | 自动完成绘制        |

#### drawCircle - 绘制圆形

| 点        | 说明               |
| --------- | ------------------ |
| 第 1 个点 | 圆心               |
| 第 2 个点 | 计算半径，自动完成 |

---

### 4. 点击获取坐标模式（含撤销功能）

#### addClickPoint - 添加点击点

```typescript
const addClickPoint = (point: any) => {
  clickPoints.value.push(point);
  // 创建并添加标记到地图
  clickMarkers.value.push(marker);
};
```

#### undoLastClickPoint - 撤销最后一个点击点 新增

**功能说明**: 撤销点击模式下最后添加的坐标点

```typescript
const undoLastClickPoint = () => {
  if (clickPoints.value.length === 0) return;

  // 1. 从数组中移除
  clickPoints.value.pop();

  // 2. 从地图移除标记
  if (clickMarkers.value.length > 0) {
    const marker = clickMarkers.value.pop();
    map.value.remove(marker);
  }

  console.log("撤销最后一个点击点");
};
```

**触发方式**:

- 按钮点击: "撤销最后一点"
- 快捷键: Ctrl+Z (在点击模式下)

#### clearClickPoints - 清除所有点击点

```typescript
const clearClickPoints = () => {
  clickMarkers.value.forEach((marker) => {
    map.value.remove(marker);
  });
  clickMarkers.value = [];
  clickPoints.value = [];
};
```

---

### 5. 键盘事件处理

```typescript
const handleKeyDown = (e: KeyboardEvent) => {
  if ((e.ctrlKey || e.metaKey) && (e.key === "z" || e.key === "Z")) {
    if (clickMode.value) {
      undoLastClickPoint(); // 点击模式：撤销点击点
    } else {
      undoLastPoint(); // 绘制模式：撤销绘制点
    }
  }
};
```

---

### 6. 数据导出

#### exportClickData - 导出点击数据

导出格式:

```json
{
  "timestamp": "ISO时间",
  "type": "click_points",
  "points": [
    {
      "index": 1,
      "longitude": 116.397,
      "latitude": 39.909,
      "coordinates": [116.397, 39.909]
    }
  ]
}
```

#### exportDrawData - 导出绘制数据

导出图形的坐标信息。

---

## 模板结构

```
container
├── sidebar
│   ├── control-panel (控制面板)
│   │   ├── 绘制模式按钮组
│   │   ├── 坐标获取按钮组 (含撤销按钮)
│   │   └── 操作按钮组
│   └── coordinates-panel (坐标显示)
└── map-container
    ├── AddressSearch
    ├── map
    └── map-info
```

---

## 返回值 (setup return)

| 属性/方法          | 说明               |
| ------------------ | ------------------ |
| currentDrawMode    | 当前绘制模式       |
| clickMode          | 点击模式状态       |
| clickPoints        | 点击坐标列表       |
| setDrawMode        | 设置绘制模式       |
| toggleClickMode    | 切换点击模式       |
| undoLastClickPoint | 撤销最后一个点击点 |
| clearClickPoints   | 清除点击点         |
| ...其他方法        | ...                |

---

## 关键注意事项

1. **高德地图 API 全局变量**: 通过 `window.AMap` 访问
2. **临时图形清理**: 每次切换模式前必须调用 `clearTempShape()`
3. **点击模式撤销**: 新增功能，需同步维护 clickPoints 和 clickMarkers
4. **键盘快捷键**: Ctrl+Z 在不同模式下有不同行为

---

## 相关文档

- [项目架构总览](./p0-architecture-overview.md)
- [地址搜索组件](./p1-address-search.md)
- [类型定义文档](./p1-types-definition.md)
