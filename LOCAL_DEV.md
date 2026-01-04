# 本地开发说明

## 问题说明

如果使用 `npm run dev` 运行本地开发服务器，API 路由（`/api/stock/*` 和 `/api/ai/*`）无法工作，因为这些是 Vercel Serverless Functions，需要 Vercel 环境才能运行。

## 解决方案：使用 Vercel CLI

### 1. 安装 Vercel CLI

```bash
npm install -g vercel
```

或者使用 npx（无需全局安装）：

```bash
npx vercel dev
```

### 2. 运行本地开发服务器

```bash
npm run dev:vercel
```

或者直接运行：

```bash
vercel dev
```

### 3. 首次运行配置

首次运行 `vercel dev` 时，会提示你：
- 链接到现有项目（Link to existing project）或创建新项目（Create new project）
- 选择项目范围（Project scope）
- 确认项目设置（Project settings）

建议选择 "Link to existing project"，如果还没有项目，可以选择 "Create new project"。

### 4. 环境变量配置

Vercel CLI 会自动从项目根目录的 `.env` 文件加载环境变量。

确保你的 `.env` 文件包含：

```
GEMINI_API_KEY=你的_Gemini_API_密钥
DEEPSEEK_API_KEY=你的_DeepSeek_API_密钥
JUHE_API_KEY=你的_聚合数据_API_密钥
QWEN_API_KEY=你的_通义千问_API_密钥
```

## 为什么需要 Vercel CLI？

- `api/` 目录下的文件是 Vercel Serverless Functions
- 这些函数只在 Vercel 运行时环境中执行
- `vercel dev` 会启动一个本地 Vercel 环境，模拟生产环境
- 这样 API 路由和前端都可以在本地正常运行

## 替代方案

如果你想继续使用 `npm run dev`，你需要：
1. 将 API 路由迁移到其他框架（如 Express）
2. 或者使用代理服务器将 `/api/*` 请求转发到远程服务器

但推荐使用 `vercel dev`，因为它与生产环境最接近。

