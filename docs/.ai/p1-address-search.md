# AddressSearch 组件详解

## 概述

`AddressSearch.vue` 是地址搜索组件，提供地址/POI 搜索功能，并支持搜索结果展示和位置定位。

**文件位置**: `src/components/AddressSearch.vue`

---

## 组件 Props & Events

### Emits (事件)

| 事件名 | 参数 | 说明 |
|--------|------|------|
| `location-selected` | `{ lng: number, lat: number }` | 选择位置时触发 |

---

## 状态变量

| 变量名 | 类型 | 说明 |
|--------|------|
| searchValue | ref&lt;string&gt; | 搜索输入框的值 |
| searchResults | ref&lt;SearchResult[]&gt; | 搜索结果列表 |
| isSearching | ref&lt;boolean&gt; | 是否正在搜索 |
| error | ref&lt;string&gt; | 错误信息 |
| autoComplete | ref&lt;any&gt; | 高德 AutoComplete 实例 |
| placeSearch | ref&lt;any&gt; | 高德 PlaceSearch 实例 |

---

## SearchResult 接口

```typescript
interface SearchResult {
  id: string;
  name: string;
  address: string;
  location: {
    lng: number;
    lat: number;
  };
}
```

---

## 核心功能

### 1. 初始化搜索服务 (initSearchServices)

```typescript
onMounted(() => {
  if (window.AMap) {
    window.AMap.plugin(['AMap.PlaceSearch', 'AMap.AutoComplete'], () => {
      initSearchServices();
    });
  }
});
```

**加载的插件**:
- `AMap.AutoComplete - 输入提示
- `AMap.PlaceSearch - 地点搜索

---

### 2. 自动完成 (AutoComplete)

```typescript
const autoOptions = {
  input: "tipinput"
};
autoComplete.value = new window.AMap.AutoComplete(autoOptions);
autoComplete.value.on("select", handleAutoCompleteSelect);
```

**功能**:
- 监听输入框
- 提供输入时显示建议
- 选择建议后触发搜索

---

### 3. 地点搜索 (PlaceSearch)

```typescript
placeSearch.value = new window.AMap.PlaceSearch({
  pageSize: 10,
  pageIndex: 1,
  citylimit: false
});
```

**配置项**:
- `pageSize`: 每页结果数
- `pageIndex`: 页码
- `citylimit`: 是否限制城市

---

### 4. 搜索流程

```
用户输入关键词
    ↓
AutoComplete 提示（可选）
    ↓
回车或点击搜索按钮
    ↓
performPlaceSearch()
    ↓
显示搜索结果
    ↓
用户选择结果
    ↓
emit 'location-selected' 事件
```

---

## 模板结构

```
.address-search
├── .search-container
│   ├── input#tipinput (搜索输入框)
│   └── .search-button (搜索按钮)
├── .search-results (搜索结果列表)
│   └── .result-item (单个结果)
├── .searching-indicator (搜索中提示)
└── .search-error (错误提示)
```

---

## 样式说明

组件样式内联在组件中，包括：
- 搜索框样式
- 搜索结果下拉列表
- 加载动画
- 响应式布局

---

## 与 MapDrawer 交互

```vue
<!-- MapDrawer.vue 中使用 -->
<AddressSearch @location-selected="handleLocationSelected" />
```

`handleLocationSelected` 函数会:
1. 平滑移动地图到选择的位置
2. 显示临时标记
3. 3秒后移除标记

---

## 相关文档

- [MapDrawer 组件详解](./p0-map-drawer.md)
- [项目架构总览](./p0-architecture-overview.md)
