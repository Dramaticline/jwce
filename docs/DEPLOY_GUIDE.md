# JWCE 部署指南 —— 从零到 GitHub Pages 上线

> 目标：把 JWCE 项目部署到 GitHub Pages，拿到一个公网 URL，供 PWABuilder 检测并生成 APK。
> 预计耗时：**10~20 分钟**（不含 PWABuilder 打包时间）
> 难度：**⭐⭐ 入门级**（无需服务器、无需域名、无需付费）

---

## 目录

- [前置准备](#前置准备)
- [Step 1：创建 GitHub 仓库](#step-1创建-github-仓库)
- [Step 2：上传项目文件](#step-2上传项目文件)
- [Step 3：开启 GitHub Pages](#step-3开启-github-pages)
- [Step 4：验证部署成功](#step-4验证部署成功)
- [Step 5：PWABuilder 生成 APK](#step-5pwabuilder-生成-apk)
- [常见问题排查](#常见问题排查)
- [后续更新流程](#后续更新流程)

---

## 前置准备

| 项目 | 要求 | 说明 |
|------|------|------|
| GitHub 账号 | 免费即可 | [github.com/join](https://github.com/join) |
| 项目文件 | 本压缩包内全部文件 | 解压后得到 `jwce-pwa-release/` 文件夹 |
| 网络 | 能访问 github.com | 国内用户如访问慢，可用代理 |
| 浏览器 | Chrome / Edge 最新版 | 用于 PWABuilder 检测 |

**不需要准备的东西**：服务器、域名、SSL 证书、Android Studio、Java 环境、签名密钥。

---

## Step 1：创建 GitHub 仓库

1. 打开浏览器，登录 GitHub，点击右上角 **+** → **New repository**

   ```
   https://github.com/new
   ```

2. 填写仓库信息（**这一步直接影响你的访问地址，务必照填**）：

   | 字段 | 填什么 | 注意事项 |
   |------|--------|----------|
   | **Repository name** | `jwce` | ⚠️ 必须小写，建议就叫 jwce |
   | **Description** | `JWCE - 本地优先的情侣日常记录 PWA` | 选填 |
   | **Public / Private** | ✅ **Public** | ⚠️ **必须选 Public**，Private 仓库无法用免费 Pages |
   | **Add a README** | ❌ 不要勾 | 压缩包里已有 README.md |
   | **Add .gitignore** | ❌ 不要勾 | 压缩包里已有 |
   | **Choose a license** | ❌ 不要勾 | 压缩包里已有 LICENSE |

3. 点击绿色按钮 **Create repository**

4. 创建成功后，你会看到一个**空的仓库页面**，地址栏类似：

   ```
   https://github.com/你的用户名/jwce
   ```

   **把这个地址记下来，后面要用。**

---

## Step 2：上传项目文件

> 两种方式二选一。**新手强烈推荐方式 A**（网页拖拽，无需装软件）。

### 方式 A：网页拖拽上传（推荐新手）

1. 在刚创建的空仓库页面，点击 **uploading an existing file**（或在地址栏末尾加 `/upload`）

2. **关键：不要上传外层文件夹**，只上传文件夹**里面**的内容。

   ❌ 错误做法：把 `jwce-pwa-release` 整个文件夹拖进去
   ✅ 正确做法：打开 `jwce-pwa-release` 文件夹，把里面的**所有文件和文件夹**一起选中拖进去

   应该看到这些文件出现在上传区：

   ```
   ✓ index.html
   ✓ manifest.json
   ✓ sw.js
   ✓ offline.html
   ✓ LICENSE
   ✓ README.md
   ✓ CONTRIBUTING.md
   ✓ PRIVACY.md
   ✓ SECURITY.md
   ✓ .gitignore
   ✓ icons/          （这是个文件夹，会整体上传）
   ✓ docs/
   ✓ .github/
   ```

3. 在 **Commit changes** 区域：

   | 字段 | 填什么 |
   |------|--------|
   | **Commit message** | `feat: 初始化 JWCE PWA 项目` |
   | **Description** | 留空即可 |
   | **分支** | 保持默认的 `main` |

4. 点击 **Commit changes**（绿色按钮）

5. 等待上传完成（文件较多时约 30 秒~2 分钟），页面会自动刷新

### 方式 B：Git 命令行（适合有 Git 基础的用户）

```bash
# 1. 解压后进入项目目录
cd jwce-pwa-release

# 2. 初始化仓库
git init

# 3. 添加所有文件
git add .

# 4. 提交
git commit -m "feat: 初始化 JWCE PWA 项目"

# 5. 关联远程仓库（把「你的用户名」替换成实际的）
git remote add origin https://github.com/你的用户名/jwce.git

# 6. 推送到 GitHub
git push -u origin main
```

> 如果推送时报错 `src refspec main does not match`，说明你的默认分支叫 `master`，把最后一句改成：
> ```bash
> git branch -M main
> git push -u origin main
> ```

---

## Step 3：开启 GitHub Pages

1. 进入仓库页面，点击顶部导航的 **Settings**（齿轮图标）

2. 在左侧菜单找到并点击 **Pages**

3. 在 **Build and deployment** 区域，按如下配置：

   | 配置项 | 选择 |
   |--------|------|
   | **Source** | ✅ **Deploy from a branch** |
   | **Branch** | ✅ **main** |
   | **Folder** | ✅ **/ (root)** |
   | **Enforce HTTPS** | ✅ 保持勾选（默认就是） |

4. 点击 **Save**

5. 页面会刷新，顶部出现一个黄色提示：

   > GitHub Pages is currently disabled. We'll let you know when it's ready.

   **等 1~3 分钟**，刷新页面。当看到类似下面的绿色提示时，说明部署成功：

   > ✅ **Your site is live at** `https://你的用户名.github.io/jwce/`

---

## Step 4：验证部署成功

按以下顺序**逐项验证**，任何一步失败都先解决再往下走。

### 4.1 访问主页

打开浏览器，访问：

```
https://你的用户名.github.io/jwce/
```

✅ 成功：看到 JWCE 应用界面
❌ 失败：显示 404 → 跳到 [常见问题排查](#常见问题排查) Q1

### 4.2 验证 manifest 可访问

浏览器地址栏输入：

```
https://你的用户名.github.io/jwce/manifest.json
```

✅ 成功：直接显示一段 JSON 文本（就是 manifest.json 的内容）
❌ 失败：404 或下载失败 → 说明文件没上传成功，回 Step 2 检查

### 4.3 验证图标可访问

```
https://你的用户名.github.io/jwce/icons/icon-192.png
```

✅ 成功：浏览器显示一张 192×192 的 JW 图标
❌ 失败：404 → 检查 icons 文件夹是否上传成功

### 4.4 验证 Service Worker

1. 打开主页 `https://你的用户名.github.io/jwce/`
2. 按 `F12` 打开开发者工具
3. 切到 **Application** 标签 → 左侧 **Service Workers**
4. 应该看到 `sw.js` 处于 **Activated and running** 状态

✅ 成功：sw.js 状态正常
❌ 失败：看不到 sw.js → 检查 sw.js 是否上传、浏览器是否支持 SW

### 4.5 验证离线能力

1. 在开发者工具的 **Network** 标签，把 **No throttling** 改为 **Offline**
2. 刷新页面

✅ 成功：页面仍能正常显示（Service Worker 返回离线页面）
❌ 失败：显示「无法访问此网站」→ SW 未注册成功

**以上 5 项全部通过后，再进行下一步。**

---

## Step 5：PWABuilder 生成 APK

现在你的项目已经有公网地址了，可以交给 PWABuilder 处理。

### 5.1 打开 PWABuilder

```
https://www.pwabuilder.com/
```

### 5.2 输入 URL

在首页大输入框里，输入你的 Pages 地址：

```
https://你的用户名.github.io/jwce/
```

⚠️ **三个易错点**：

| 易错点 | 后果 |
|--------|------|
| 末尾漏了 `/` | 可能检测到错误的 start_url |
| 用了 `http://` | Pages 强制 HTTPS，会跳转导致检测失败 |
| 用了仓库地址 `github.com/...` | 那是代码仓库，不是网页 |

### 5.3 开始检测

点击 **Start** 按钮，等待 10~30 秒。

**期望结果**：看到三个绿色大圆球

```
🟢 PWA 检测项
🟢 iOS 支持
🟢 Android 支持
```

⚠️ 如果看到红色错误，先看 [常见问题排查](#常见问题排查) Q3。

### 5.4 生成 APK

1. 点击 **Android** 卡片（或 "Generate Android Package" 按钮）
2. 进入配置页，推荐配置如下：

   | 配置项 | 推荐值 | 说明 |
   |--------|--------|------|
   | **Package ID** | `com.jwce.app` | 反向域名格式，可自定义 |
   | **App Name** | `JWCE` | 手机上显示的应用名 |
   | **Language** | `Java` / `Kotlin` 均可 | 不影响功能 |
   | **Signing** | `No signing`（测试版） | 想上架应用商店再选 `New` |
   | **Include source code** | ✅ 勾选 | 方便二次开发 |

3. 点击 **Generate** 或 **Download**
4. 等待 1~3 分钟，浏览器自动下载一个 ZIP 包

### 5.5 下载 APK

1. 解压下载的 ZIP 包
2. 找到 `app-release.apk`（或 `app-debug.apk`）文件
3. 把这个 APK 传到手机上安装即可

> 如果选了 `No signing`，安装时手机可能提示「未知来源应用」，需要在设置里允许。

---

## 常见问题排查

### Q1：访问 Pages 地址显示 404

**按以下顺序排查**：

1. 仓库是否是 **Public**？Private 仓库无法使用免费 Pages
2. 文件名是否准确？必须是 `index.html`（注意大小写，不能是 `Index.html`）
3. `index.html` 是否在**仓库根目录**，而不是在某个子文件夹里
4. Pages 设置里的 Branch 是否是 `main`，Folder 是否是 `/ (root)`
5. 等待时间是否足够？首次部署有时需要 5 分钟

### Q2：manifest.json 能访问，但 PWABuilder 报错

**90% 的情况是 URL 填错了**，对照检查：

| 错误填法 | 正确填法 |
|----------|----------|
| `github.com/用户名/jwce` | `https://用户名.github.io/jwce/` |
| `https://github.com/用户名/jwce/tree/main` | `https://用户名.github.io/jwce/` |
| `https://用户名.github.io/jwce` | `https://用户名.github.io/jwce/`（补 `/`） |

### Q3：PWABuilder 报图标相关错误

这个项目已经通过 PWABuilder 的图标检测（10 个图标、type 字段、maskable 全部合规）。**如果还报错，几乎肯定是 URL 问题**，不是代码问题。

**强制刷新缓存**：在 PWABuilder 页面按 `Ctrl + F5`（Mac 为 `Cmd + Shift + R`），然后重新输入 URL。

### Q4：GitHub Pages 部署成功，但图标还是 404

通常是**浏览器缓存**或 **CDN 缓存**问题：

1. 强制刷新：`Ctrl + F5`
2. 无痕模式打开 Pages 地址
3. 等待 5 分钟让 CDN 缓存刷新

### Q5：手机安装 APK 提示「应用未安装」

可能原因：

- 之前装过旧版本，签名不一致 → **先卸载旧版本**再装
- 选了 `No signing` → 部分手机拒绝未签名应用，改用 `New` 生成签名版
- 手机 Android 版本过低 → PWABuilder 生成的 APK 最低支持 Android 5.0

### Q6：应用能打开，但通知不响

PWA 的通知依赖**浏览器引擎**，需要：

1. 手机上用 **Chrome** 或 **Edge** 打开过一次应用
2. 在应用内点「允许通知」时点了**允许**（不是拒绝）
3. 手机系统设置 → 应用管理 → 找到 Chrome → 允许通知

### Q7：仓库名不想叫 jwce

可以叫别的，比如 `my-couple-app`。但要注意**三处同步修改**：

1. **仓库名**：在 GitHub 仓库 Settings → General → Repository name 里改
2. **访问地址**：会变成 `https://用户名.github.io/新仓库名/`
3. **PWABuilder 输入的 URL**：同步改成新地址

**不需要改代码**。manifest 里的路径都是绝对路径 `/xxx`，与仓库名无关。

---

## 后续更新流程

改完代码后，推送到 GitHub 即可，**Pages 会自动重新部署**（约 1~2 分钟生效）。

### 网页拖拽方式

1. 在仓库页面点 **Add file** → **Upload files**
2. 只上传**改动过的文件**（不用全部重传）
3. 填写 Commit message，如 `fix: 修复图标显示问题`
4. 点 **Commit changes**
5. 等 1~2 分钟，访问 Pages 地址确认更新

### Git 命令行方式

```bash
cd jwce-pwa-release

# 查看改动
git status

# 添加改动文件
git add 改动的文件名

# 提交
git commit -m "fix: 修复图标显示问题"

# 推送
git push
```

### 重新生成 APK

代码更新后，APK 需要**重新生成**：

1. 回到 [PWABuilder](https://www.pwabuilder.com/)
2. 重新输入 Pages URL
3. 走完检测 → 生成 APK 流程
4. 卸载手机上的旧 APK，安装新 APK

> 如果选了 `New` 签名方式，建议**保存好签名密钥**，这样多次生成的 APK 可以覆盖安装，不用卸载旧版。

---

## 附录：关键地址速查

部署完成后，你会用到这几个地址：

| 用途 | 地址模板 |
|------|----------|
| **代码仓库** | `https://github.com/你的用户名/jwce` |
| **在线应用** | `https://你的用户名.github.io/jwce/` |
| **manifest** | `https://你的用户名.github.io/jwce/manifest.json` |
| **PWABuilder** | `https://www.pwabuilder.com/` |
| **仓库设置** | `https://github.com/你的用户名/jwce/settings/pages` |

---

**下一步建议**：部署成功后，可以打开 `docs/PWABUILDER_GUIDE.md` 查看 APK 签名管理和上架应用商店的详细步骤。
