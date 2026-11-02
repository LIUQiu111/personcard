# 初开 · ChuKai — 个人名片页

单文件静态名片，零依赖（仅 Google Fonts CDN），可直接丢到 GitHub Pages / Cloudflare Pages / Vercel / 任意静态托管。

## 结构

```
chukai-card/
├── index.html              # 全部内容：CSS + HTML + JS 内联，单文件
├── .nojekyll               # 告诉 GitHub Pages 不要走 Jekyll
├── README.md
├── assets/                 # 预留：头像、og 分享图
└── .github/
    └── workflows/
        └── pages.yml       # 推送 main 自动部署 Pages
```

## 本地预览

不需要构建。直接双击 `index.html`，或：

```bash
python3 -m http.server 8000
# 打开 http://localhost:8000
```

## 部署到 GitHub Pages（两种方式，选一个）

### 方式 A：仓库根目录直接发布（最简单，推荐先用这个）

```bash
cd chukai-card
git init -b main
git add -A
git commit -m "init: personal card"
gh repo create chukai-card --public --source=. --remote=origin --push
```

然后到 GitHub 仓库 → **Settings → Pages**：
- Source 选 **Deploy from a branch**
- Branch 选 `main`，目录选 `/ (root)`
- 保存，等 1 分钟

地址：`https://<你的用户名>.github.io/chukai-card/`

> 如果用了方式 A，请把 `.github/workflows/pages.yml` 删掉，避免两套部署冲突。

### 方式 B：用 Actions 部署

保留 `.github/workflows/pages.yml`，推送后在 **Settings → Pages → Source** 里选 **GitHub Actions** 即可。

## 绑定自定义域名

1. 域名 DNS 加一条 CNAME：`card.chukai.cc` → `<用户名>.github.io`
2. 在 `assets/` 同级建一个 `CNAME` 文件，内容只有一行：
   ```
   card.chukai.cc
   ```
3. 仓库 Settings → Pages → Custom domain 填入 `card.chukai.cc`，勾选 **Enforce HTTPS**
4. 同时把 `index.html` 里的 `<meta property="og:url" content="https://chukai.cc">` 改成你的名片地址

Cloudflare 那边记得把这条 CNAME 设为 **DNS only（灰云）**，否则 GitHub 的证书签发会卡住。

## 需要你补的地方（都在 index.html 里搜关键字）

| 位置 | 关键字 | 说明 |
|---|---|---|
| — | `liuqiu2778680280@gmail.com` | 邮箱已填（3 处：`EMAIL` 变量、`mailto:` ×2、`small` 展示）。换邮箱时全局替换即可 |
| head | `og:url` | 改成名片实际地址（自定义域名之后） |
| assets | — | 想换头像就把 `.avatar` 里的 `<span>CK</span>` 换成 `<img>` |

## 隐私提醒

GitHub Pages 是**公开可索引**的。这个页面上的「Android 逆向 / Frida / Xposed 检测」等关键词会把站点和你的技术方向永久关联起来，搜索引擎可能收录。如果不想被某些场景检索到，可以：

- 在 `<head>` 加 `<meta name="robots" content="noindex">`
- 或只保留「安全研究 / CTF」表述，去掉具体条目

## 内容来源

- 文章列表：`https://chukai.cc/?rest_route=/wp/v2/posts` 实时抓取（28 篇，页面展示最近 12 篇）
- GitHub：`LIUQiu111`
- 所有链接均为真实可访问地址

## 声明

页面内容仅用于授权环境下的安全研究与学习，不提供任何破解、外挂、绕过检测或未授权访问服务。