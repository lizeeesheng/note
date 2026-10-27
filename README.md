# 短信验证码看板 (note)

部署在 Cloudflare Worker 上的短信验证码收集与管理后台。支持每页 50 条分页、暗色模式、单条删除。

## 快速部署（Cloudflare Workers）

### 方式一：直接粘贴代码（最简单）
1. Cloudflare → Workers → 创建 Worker。
2. 将 `src/worker.js` 全部内容粘贴进代码编辑器并保存。
3. 在「设置 → 变量」绑定 KV Namespace，Variable name 填 `NOTE-KV`（未创建则先新建）。
4. 部署后访问 `/admin` 登录即可。

### 方式二：Fork + Wrangler
1. Fork 本仓库。
2. `npx wrangler login`。
3. 在 `wrangler.toml` 中把 KV `id` 换成你自己的命名空间 ID。
4. `npx wrangler deploy`。

## 使用说明
- 收集：`https://域名/?collect=验证码`
- 后台：`/admin`（账号与口令在 `src/worker.js` 顶部，部署前请自行修改）
- 分页：每页 50 条，支持翻页与跳页，每 30 秒自动刷新

## 安全提示

⚠️ 本仓库为**公开仓库**。

- `src/worker.js` 顶部的 `ADMIN_USER` / `ADMIN_PASS` / `ADMIN_TOKEN` 是占位值，**部署前必须改成你自己的强口令**。
- 切勿把真实凭据提交进本仓库；一旦提交，任何访问本仓库的人都能直接登录你的后台。
