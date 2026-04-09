# 样式指南

## 概述

本文档说明项目的样式规范。

---

## 样式文件位置

| 文件 | 说明 |
|------|------|
| `src/assets/map-styles.css` | 地图相关样式 |
| `src/App.vue` | 根组件样式（内联） |
| 组件内 &lt;style scoped&gt; | 组件私有样式 |

---

## CSS 类名约定

使用 BEM 风格或简单描述性命名。

### 常用类名

| 类名 | 说明 |
|------|------|
| `.container` | 容器 |
| `.sidebar` | 侧边栏 |
| `.map-container` | 地图容器 |
| `.control-panel` | 控制面板 |
| `.coordinates-panel` | 坐标显示面板 |
| `.btn` | 按钮基类 |
| `.btn-primary` | 主要按钮 |
| `.btn-secondary` | 次要按钮 |
| `.btn-warning` | 警告按钮 |
| `.btn-danger` | 危险按钮 |
| `.btn-success` | 成功按钮 |
| `.btn-info` | 信息按钮 |

---

## 按钮状态

### 激活状态 (active)

```css
.btn.active {
  /* 激活状态样式 */
}
```

### 禁用状态 (disabled)

```css
.btn:disabled {
  /* 禁用状态样式 */
  opacity: 0.6;
  cursor: not-allowed;
}
```

---

## 颜色规范

### 主色调

| 用途 | 颜色值 |
|------|--------|
| 主要按钮 | 蓝色系 |
| 警告按钮 | 黄色系 |
| 危险按钮 | 红色系 |
| 成功按钮 | 绿色系 |
| 信息按钮 | 蓝绿色系 |

### 图形颜色

| 图形 | 边框颜色 | 填充颜色 |
|------|----------|----------|
| 多边形 | #FF0000 (红) | #FF0000 |
| 矩形 | #00FF00 (绿) | #00FF00 |
| 圆形 | #0000FF (蓝) | #0000FF |

---

## 响应式设计

移动端适配:

```css
@media (max-width: 600px) {
  /* 移动端样式 */
}
```

---

## 相关文档

- [项目架构总览](./p0-architecture-overview.md)
