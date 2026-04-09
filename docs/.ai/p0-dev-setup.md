# 开发环境配置

## 前置要求

- Node.js 16+
- npm / yarn / pnpm

## 快速开始

### 1. 克隆项目

```bash
git clone <repository-url>
cd amap-coordinate-picking
```

### 2. 安装依赖

```bash
npm install
# 或
pnpm install
# 或
yarn
```

### 3. 配置高德地图 API Key

#### 方式一：环境变量文件 (推荐)

复制 `.env.example` 为 `.env`：

```bash
cp .env.example .env
```

编辑 `.env` 文件：

```env
VITE_APP_API_KEY=你的高德地图API密钥
VITE_APP_MAP_SECURITY=你的安全密钥
```

#### 方式二：直接修改配置文件

编辑 `src/config/mapConfig.ts`：

```typescript
export const MAP_CONFIG: MapConfig = {
  API_KEY: '你的API密钥',
  securityJsCode: '你的安全密钥',
  // ...
};
```

### 4. 获取高德地图 API Key

1. 访问 [高德开放平台](https://lbs.amap.com/)
2. 注册/登录账号
3. 进入「控制台」→「应用管理」→「我的应用」
4. 创建新应用，选择「Web端(JS API)」类型
5. 获取 Key 和 安全密钥 (securityJsCode)
6. **重要**：在「设置」中配置域名白名单
   - 本地开发添加: `localhost`, `127.0.0.1`
   - 部署环境添加你的域名

### 5. 启动开发服务器

```bash
npm run dev
# 或
pnpm dev
```

访问显示的本地地址（通常是 http://localhost:5173）

## 常用命令

| 命令 | 说明 |
|------|------|
| `npm run dev` | 启动开发服务器 |
| `npm run build` | 构建生产版本 |
| `npm run preview` | 预览构建结果 |

## 项目配置

### TypeScript 配置

- `tsconfig.json` - 基础 TS 配置
- `tsconfig.node.json` - Node 环境 TS 配置
- `tsconfig.app.json` - 应用 TS 配置

### Vite 配置

`vite.config.ts` - Vite 构建工具配置

## 开发注意事项

1. **API Key 安全**: 不要将 `.env` 文件提交到 Git（已在 .gitignore 中）
2. **域名白名单**: 确保开发和部署环境的域名都已配置
3. **HTTPS**: 生产环境建议使用 HTTPS
4. **网络连接**: 需要稳定的网络连接加载高德地图资源

## 下一步

- 了解核心组件：[MapDrawer 组件详解](./p0-map-drawer.md)
- 查看项目架构：[项目架构总览](./p0-architecture-overview.md)
