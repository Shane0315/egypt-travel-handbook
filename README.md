# 埃及旅行手册 · 部署与维护指南

## 一、交付物

| 文件 | 说明 |
|---|---|
| `index.html` | 单文件 HTML 旅行手册（零外部依赖，57KB） |
| `.github/workflows/deploy.yml` | Cloudflare Pages 自动部署 workflow |
| `README.md` | 本部署指南 |

页面功能：倒计时（每秒跳动）· 手绘 SVG 路线图 · 已确认预订 · 逐日行程（可展开+全天导航）· 待办清单 · 实用贴士 · 昼夜自动配色 + 手动切换 · 所有时间带时区（埃及 UTC+3 / 北京 UTC+8）。

## 二、当前线上地址（已部署）

| 站点 | 网址 | 更新方式 |
|---|---|---|
| **GitHub Pages** | https://shane0315.github.io/egypt-travel-handbook/ | push 到 main 自动更新 ✅ |
| **Cloudflare Pages** | https://egypt-travel-handbook.egypt-travel-handbook.workers.dev/ | 手动 wrangler deploy；配置 token 后可 push 自动更新 |

两个地址都是免费、公开、免登录，内容相同。

## 三、更新页面（日常操作）

### 方式 A：我改好后，你 push（推荐，GitHub Pages 自动上线）

我在本地改好 `index.html` 后，终端执行：
```bash
cd egypt-travel-handbook
git add index.html
git commit -m "update: <改了什么>"
git push origin main
```
GitHub Pages 约 30 秒自动更新，不用其他操作。

### 方式 B：push 同时更新 Cloudflare（需一次性配置 token）

要让 Cloudflare 也随 push 自动更新，需要在 Cloudflare dashboard 生成 API token 并配到 GitHub secrets：

1. 打开 https://dash.cloudflare.com/profile/api-tokens → Create Token → 用模板 **"Edit Cloudflare Workers"**（或自定义，权限含 Workers Scripts: Edit、Account: Read）
2. 创建后复制 token
3. GitHub 仓库 `egypt-travel-handbook` → Settings → Secrets and variables → Actions → 新建两个 secret：
   - `CLOUDFLARE_API_TOKEN` = 刚复制的 token
   - `CLOUDFLARE_ACCOUNT_ID` = `0eba0f5d645f6af097acef6a328d226e`
4. 之后 push 到 main 会自动触发 `.github/workflows/deploy.yml`，同时更新 GitHub Pages 和 Cloudflare Pages

> 说明：API token 是 Cloudflare 的安全凭据，必须由账号本人生成，无法由他人代劳。若不需要 Cloudflare 自动更新，跳过方式 B 即可，GitHub Pages 已完全满足「push 即上线」。

## 四、手动部署 Cloudflare（备用）

本机已通过 wrangler OAuth 登录，可手动部署：
```bash
cd egypt-travel-handbook
HTTP_PROXY= HTTPS_PROXY= http_proxy= https_proxy= ALL_PROXY= all_proxy= \
  npx wrangler@latest pages deploy . --project-name egypt-travel-handbook --branch main
```
（本机有代理环境变量时需临时清空，否则 API 请求会失败）

## 五、隐私红线（已执行）

已核对：页面不含订单号、确认号、证件号、房间号、邮箱、个人照片文件名。
保留在页面的仅限：航司名+航班号、酒店名+电话（JAZ / Le Méridien 为公开预订电话）、时间、地址、注意事项。
