# NEON DUEL

**v0.1.0**

俯视角双摇杆动作对战小游戏（单机，你 vs AI）。纯前端、零依赖、可安装 PWA。

## 运行
直接用浏览器打开 `index.html` 即可，不需要服务器、不需要构建。

## 操作
**手机**
- 左摇杆：移动（按哪儿出现在哪儿的浮动摇杆）
- 右摇杆：瞄准并自动开火
- 右下 DASH：冲刺闪避（短暂无敌，有冷却）

**电脑**
- WASD / 方向键：移动
- 鼠标：瞄准；按住左键：开火
- 空格 / Shift：冲刺

## 玩法
击破 AI 敌人进入下一轮，每轮敌人血量、射速、精准度递增。地图里的方块是掩体，子弹会被挡住，敌人也会绕掩体、躲子弹、残血后撤。

## 放到 iPhone 上当 App
用 Safari 打开网址 → 分享 → “添加到主屏幕”。已设置 `apple-mobile-web-app-capable`，并补了 `manifest.webmanifest` 和 `sw.js`，点图标会按网页 App 方式运行。

现在项目已经包含 `manifest.webmanifest` 和 `sw.js`，适合按 PWA 方式安装到主屏幕。

不想上传到 GitHub 时，有三种路线：

- 本地局域网临时测试：在 Mac 里运行 `python3 -m http.server 8000`，iPhone 和 Mac 连同一个 Wi-Fi，然后用 Safari 打开 `http://你的Mac局域网IP:8000/index.html`，再添加到主屏幕。Mac 关机或断网后这个地址就不可用。
- 长期独立网址：把这个文件夹手动上传到 Netlify Drop、Cloudflare Pages Direct Upload、Vercel CLI、对象存储静态站点等服务，不需要 GitHub 仓库。拿到 HTTPS 地址后再用 Safari 添加到主屏幕，service worker 才能稳定离线缓存。
- 真正原生 App：用 Xcode 做 SwiftUI/SpriteKit 或 WKWebView 包装，不需要网址，但需要 iOS 签名、TestFlight 或 App Store 分发流程。

## 可迭代方向
- 手感：移动/子弹速度、射速、冲刺冷却（见 `update()` 里的常量）
- 难度曲线：`setupRound()` 里的 `enemy.speed / fireRate / spread`
- 玩法扩展：多敌人、道具掉落、可破坏掩体、不同武器
- 原生移植：把逻辑搬到 SwiftUI + SpriteKit 工程，用 Xcode 跑

游戏主体逻辑都在 `index.html` 的 `<script>` 里，结构是 `update(dt)`（逻辑）+ `render()`（绘制）+ requestAnimationFrame 主循环。
