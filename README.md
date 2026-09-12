# 埃及旅行手册 · 部署与维护指南

## 一、交付物

| 文件 | 说明 |
|---|---|
| `egypt-travel-handbook/index.html` | 单文件 HTML 旅行手册（零外部依赖，57KB） |
| `egypt-travel-handbook/README.md` | 本部署指南 |

页面功能：倒计时（每秒跳动）· 手绘 SVG 路线图 · 已确认预订 · 逐日行程（可展开+全天导航）· 待办清单 · 实用贴士 · 昼夜自动配色 + 手动切换 · 所有时间带时区（埃及 UTC+3 / 北京 UTC+8）。

## 二、部署状态（2026-09-12 已完成）

### ✅ 已自动完成（无需手动操作）

- GitHub 仓库已创建并推送：https://github.com/Shane0315/egypt-travel-handbook
- **GitHub Pages 已上线：https://shane0315.github.io/egypt-travel-handbook/**
  - 公开网址，任何人点开就能看，无需登录、无需装 App
  - 免费、单 HTML、push 即自动发布
  - 已验证 HTTP 200、页面内容正确

### 更新方式（之后我改好页面，三条命令即上线）

```bash
cd egypt-travel-handbook
git add index.html
git commit -m "update: <改了什么>"
git push origin main
```

GitHub Pages 检测到 push 自动重新部署，约 30–60 秒生效。

### Cloudflare（未启用，待定）

用户最初要求 Cloudflare Workers/Pages。GitHub Pages 已满足同等需求；Cloudflare 需要用户账号授权（邮箱密码或 API Token），属于必须由本人完成的凭据步骤。若用户确认需要 Cloudflare，提供账号后 5 分钟可完成对接。

## 三、隐私红线（已执行）

已核对：页面不含订单号、确认号、证件号、房间号、邮箱、个人照片文件名。
保留在页面的仅限：航司名+航班号、酒店名+电话（JAZ / Le Méridien 为公开预订电话）、时间、地址、注意事项。
