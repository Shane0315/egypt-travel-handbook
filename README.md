# 埃及旅行手册 · 部署与维护指南

## 一、交付物

| 文件 | 说明 |
|---|---|
| `egypt-travel-handbook/index.html` | 单文件 HTML 旅行手册（零外部依赖，57KB） |
| `egypt-travel-handbook/README.md` | 本部署指南 |

页面功能：倒计时（每秒跳动）· 手绘 SVG 路线图 · 已确认预订 · 逐日行程（可展开+全天导航）· 待办清单 · 实用贴士 · 昼夜自动配色 + 手动切换 · 所有时间带时区（埃及 UTC+3 / 北京 UTC+8）。

## 二、部署方案：Cloudflare Pages + GitHub 自动发布

**推荐 Cloudflare Pages 而不是 Workers**：Pages 专为静态站点设计，连接 GitHub 后 push 即自动发布，免费额度足够个人使用，且不需要写 Worker 代码。纯静态单文件（57KB）走 Pages 是最省事的路径；若坚持用 Workers，也可把 HTML 作为 Worker 返回体托管，但没必要多一层复杂度。

### 必须由你在电脑上操作的步骤（共 6 步，一次性完成）

以下步骤**只能你亲手做**（涉及账号授权、Git 推送），我无法替你完成：

1. **创建 GitHub 仓库**（浏览器操作，约 2 分钟）
   - 打开 https://github.com/new
   - Repository name：`egypt-travel-handbook`（可自定）
   - 选 **Public**（免费 + 无需登录即可访问）
   - 不要勾选「Add a README」等初始化选项，保持空仓库
   - 点 Create repository

2. **把 HTML 文件放进仓库并推送**（终端操作，约 3 分钟）
   在你电脑的终端里执行（把 `<你的GitHub用户名>` 换成实际的）：
   ```bash
   git clone https://github.com/<你的GitHub用户名>/egypt-travel-handbook.git
   cd egypt-travel-handbook
   # 把 index.html 复制到这个目录（从交付目录拷过来）
   cp <交付目录>/egypt-travel-handbook/index.html .
   git add index.html
   git commit -m "feat: 埃及旅行手册 v1"

   git push origin main
   ```

3. **注册/登录 Cloudflare**（浏览器操作，约 2 分钟）
   - 打开 https://dash.cloudflare.com/sign-up 注册（可用邮箱）
   - 新用户免费计划即可

4. **创建 Pages 项目并连接 GitHub**（浏览器操作，约 5 分钟）
   - 登录后进入 **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
   - 首次会要求授权 Cloudflare 访问你的 GitHub（授权时选第 1 步创建的仓库）
   - 选择 `egypt-travel-handbook` 仓库
   - 构建设置：**Framework preset 选 "None"**，**Build command 留空**，**Build output directory 填 `/`**（或 `index.html` 所在目录）
   - 点 **Save and Deploy**

5. **等待首次部署完成**（约 1 分钟）
   - 部署成功后 Cloudflare 会给你一个 `xxx.pages.dev` 的网址
   - 打开验证页面正常显示

6. **（可选）绑定自定义域名**
   - 在 Pages 项目 → Custom domains 里添加
   - 若你有域名，按提示在域名服务商处加 CNAME 记录

### 之后每次更新（自动发布）

以后我改好页面后，你在终端执行：
```bash
cd egypt-travel-handbook
cp <交付目录>/egypt-travel-handbook/index.html .
git add index.html
git commit -m "update: <改了什么>"
git push origin main
```
Cloudflare 检测到 push 会自动重新部署，约 30 秒生效，不用再手动操作。

## 三、需要我每次交付时做的

你更新数据后告诉我，我改好 `index.html` 放回交付目录。你只需要执行上面的 `git add / commit / push` 三行命令。

## 四、隐私红线（已执行）

已核对：页面不含订单号、确认号、证件号、房间号、邮箱、个人照片文件名。
保留在页面的仅限：航司名+航班号、酒店名+电话（JAZ / Le Méridien 为公开预订电话）、时间、地址、注意事项。
