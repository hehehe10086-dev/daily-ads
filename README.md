# 日产广告 · Daily Ads

> 3 张照片 → 一支广告。让广告像朋友圈一样，每天都发。

一个完全在浏览器里跑的 AI 广告视频生成工具。上传 3 张实景照片，填一句卖点，选一个调性——3 分钟后拿到一支 15 秒竖屏电影级广告视频。无需注册，无需后端，无需 API key。

面向中小老板 / 店家 / 品牌主理人——餐饮、茶饮、美业、零售、本地生活都能用。

---

## 在线体验

把这个仓库部署到 GitHub Pages 之后，直接打开网址就能用。

- 📸 **上传照片**：产品图 + 环境图 + 细节图
- ✍️ **填写信息**：品牌名、一句卖点、CTA
- 🎬 **选一个调性**：时尚高级 / 温暖治愈 / 潮流动感 / 简约现代
- 📥 **下载 MP4 视频**：1080×1920 · 手机原生播放 · 直接发朋友圈 / 抖音 / 视频号 / 小红书

---

## 部署到 GitHub Pages（5 分钟搞定）

### 方法 1：网页操作（推荐，不用命令行）

1. 登录 [github.com](https://github.com)，点右上角 `+` → **New repository**
2. 仓库名填 `daily-ads`（或任意你喜欢的名字），选 **Public**，**不要**勾 "Add a README file"，点 **Create repository**
3. 在新建的仓库页面，点 **uploading an existing file**（或拖拽文件到页面上）
4. 把这个文件夹里的 **所有文件**（`index.html`、`README.md`、`.nojekyll` 等）一起拖进去
5. 底部点 **Commit changes**
6. 进入仓库的 **Settings** → 左侧 **Pages**
7. 在 **Source** 下选 **Deploy from a branch**，Branch 选 `main`，文件夹选 `/ (root)`，点 **Save**
8. 等 1-2 分钟，页面顶部会出现你的网址：
   ```
   https://你的用户名.github.io/daily-ads/
   ```
9. 把这个链接发给客户 / 朋友圈 / 投资人就可以了 ✅

### 方法 2：命令行（如果你会用 git）

```bash
cd daily-ads
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/你的用户名/daily-ads.git
git push -u origin main
```

然后去仓库 Settings → Pages 启用即可。

---

## 自定义域名（可选进阶）

如果你有自己的域名（比如 `dailyads.com`），可以绑到 GitHub Pages 上：

1. 在仓库根目录加一个文件叫 `CNAME`，里面只写你的域名（比如 `dailyads.com`）
2. 在域名服务商那里加一条 `CNAME` 记录指向 `你的用户名.github.io`
3. 仓库 Settings → Pages → Custom domain 填上你的域名 → 勾 Enforce HTTPS

这样链接就变成 `https://dailyads.com` 了——发给客户更正式。

---

## 技术实现

这是一个**单文件静态应用**——只有一个 `index.html`，没有 build 流程，没有依赖，打开就能跑。核心技术：

| 模块 | 实现 |
|------|------|
| 视频渲染 | HTML5 Canvas 1080×1920 实时绘制 |
| 运镜 | Ken Burns + crashZoom + whipPan + 视差焦外模糊 |
| 调色 | 多层 `globalCompositeOperation` 堆叠模拟 LUT |
| 字幕动效 | 字符级关键帧（revealChars / kineticType / slamIn / wordFade / slideLeft） |
| 背景音乐 | Web Audio API 实时合成（4 套调性专属编曲） |
| **视频导出** | **WebCodecs `VideoEncoder` + `AudioEncoder` + `mp4-muxer` → MP4 (H.264 + AAC)** |
| 备用路径 | 旧浏览器自动回退到 `MediaRecorder` WebM |
| 字体 | Google Fonts CDN（Noto Serif SC / Instrument Serif / JetBrains Mono） |

全部逻辑在客户端执行——用户隐私不上传任何地方，服务器成本为零，无限扩展。

**为什么是 MP4？** iPhone 原生不播 WebM，微信朋友圈 / 抖音 / 视频号上传 WebM 会被拒。MP4（H.264 + AAC）是手机和所有社交平台通吃的唯一格式。

---

## 本地开发

直接双击 `index.html` 用浏览器打开就行。或者启动一个本地服务器：

```bash
# Python
python3 -m http.server 8000

# 或 Node.js
npx serve .
```

然后访问 `http://localhost:8000`。

推荐 Chrome / Edge 最新版——Safari 对 `MediaRecorder` 的 WebM 支持有限，可能导出失败。

---

## 适用场景

- 🍵 **餐饮 / 茶饮**：新品上架、周年庆、节日活动、限时折扣
- ✂️ **美业 / 美发**：新技师到店、会员活动、项目推广
- 🛍️ **零售 / 服饰**：新款上新、换季清仓、爆款复购
- 🏠 **本地生活**：门店日常、客户好评、招商加盟、招聘启事
- 📦 **电商 / 微商**：主推品上架、大促预热、回购激励

---

## License

MIT — 自由使用、修改、商用。

---

Made with AI in China · 2026
