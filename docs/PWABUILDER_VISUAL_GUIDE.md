# 📸 PWABuilder 图文操作指南（独立版）

> **本文档独立成文**，不依赖其他指南，照着做即可从零生成 JWCE 的 Android APK。
> 适合：零 Android 开发经验、不想装 Android Studio、只想快速拿到安装包的用户。
> 预计耗时：**10~15 分钟**（前提是已完成 GitHub Pages 部署）。

---

## 📋 开始前：确认一件事

你必须**已经**有一个能公网访问的 JWCE 地址，类似这样：

```
https://你的用户名.github.io/jwce/
```

如果还没有，请先完成部署。**本文档不涉及部署步骤。**

**自检方法**：浏览器打开上面这个地址，能看到 JWCE 应用界面，就算通过。

---

## 🚀 完整图文步骤

### Step 1：打开 PWABuilder 官网

1. 浏览器访问 **[https://www.pwabuilder.com/](https://www.pwabuilder.com/)**
2. 你会看到一个简洁的首页，中央有一个大输入框

**页面长这样**：

```
┌─────────────────────────────────────────────────┐
│  PWABuilder                           [Sign in] │
│                                                 │
│         🚀 Your PWA,             ▲             │
│            native apps.           │             │
│                                  │             │
│  ┌───────────────────────────────────────┐     │
│  │  🔗 URL to your PWA                   │     │
│  │  https://你的用户名.github.io/jwce/  │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│              [  Start  ]                        │
│                                                 │
│  What is a PWA?  |  Documentation  |  Blog     │
└─────────────────────────────────────────────────┘
```

> **要点**：输入框里填的就是你的 GitHub Pages 地址。

---

### Step 2：输入 URL 并点击 Start

在输入框中填入（**照抄，只改用户名**）：

```
https://你的用户名.github.io/jwce/
```

> **三个坑，务必注意**：
> - 必须以 `https://` 开头（不是 `http://`）
> - 必须以 `/` 结尾（末尾有斜杠）
> - 仓库名 `jwce` 必须和实际仓库名一致

填好后，点击 **Start** 按钮（或按 Enter）。

---

### Step 3：等待检测完成

点击 Start 后，PWABuilder 会开始分析你的 PWA，大约等待 **10~30 秒**。

**你会看到一个检测仪表盘，长这样**：

```
┌─────────────────────────────────────────────────┐
│  📊 Analysis Results                            │
│                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐      │
│  │   🟢     │  │   🟢     │  │   🟢     │      │
│  │  PWA     │  │  iOS     │  │ Android  │      │
│  │  Ready   │  │  Ready   │  │  Ready   │      │
│  └──────────┘  └──────────┘  └──────────┘      │
│                                                 │
│  ─────────────────────────────────────────────  │
│                                                 │
│  ✅ HTTPS enabled                               │
│  ✅ Web App Manifest found                      │
│  ✅ Service Worker registered                   │
│  ✅ Icons (10 found, includes 512x512)          │
│  ✅ Maskable icons provided                     │
│  ✅ Theme color set                             │
│  ✅ Apple touch icons                           │
│                                                 │
│              [  Build My PWA  ]                  │
│                                                 │
└─────────────────────────────────────────────────┘
```

**正常结果应该是全部 🟢 或 ✅**。

| 检测项 | 预期状态 | 说明 |
|--------|----------|------|
| HTTPS | ✅ Pass | GitHub Pages 默认支持 |
| Web App Manifest | ✅ Pass | JWCE 的 manifest.json 已配置完整 |
| Service Worker | ✅ Pass | sw.js 已实现缓存 |
| Icons | ✅ Pass | 10 个尺寸图标已就绪 |
| Apple Touch Icons | ✅ Pass | apple-touch-icon.png 已配置 |
| Theme Color | ✅ Pass | `#f6efe9` 已设置 |

> 如果某项 ❌ Fail，**不要跳过**，直接翻到本文档末尾的 [常见问题](#-常见问题) 排查。

---

### Step 4：点击 "Build My PWA"

在检测仪表盘页面，找到并点击绿色大按钮 **"Build My PWA"**。

**进入平台选择页**：

```
┌─────────────────────────────────────────────────┐
│  📱 Choose a platform                           │
│                                                 │
│  ┌────────────────┐  ┌────────────────┐        │
│  │  🤖 Android    │  │  🍎 iOS       │        │
│  │  Recommended   │  │               │        │
│  │                │  │               │        │
│  │  [ Select ]    │  │  [ Select ]   │        │
│  └────────────────┘  └────────────────┘        │
│                                                 │
│  ┌────────────────┐                             │
│  │  💻 Windows    │                             │
│  │  [ Select ]    │                             │
│  └────────────────┘                             │
│                                                 │
└─────────────────────────────────────────────────┘
```

**点击 Android 卡片**（本次只打 Android 包）。

---

### Step 5：填写 Android 打包参数

进入配置页面后，你会看到一堆表单字段。**按下面表格逐项填写**：

```
┌─────────────────────────────────────────────────┐
│  ⚙️ Android Package Options                     │
│                                                 │
│  App Name                                       │
│  ┌───────────────────────────────────────┐     │
│  │  JWCE                                  │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  Package ID                                     │
│  ┌───────────────────────────────────────┐     │
│  │  app.jwce.couple                       │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  App Version        App Version Code            │
│  ┌───────────────┐  ┌───────────────┐         │
│  │  1.0.0         │  │  1             │         │
│  └───────────────┘  └───────────────┘         │
│                                                 │
│  Start URL                                      │
│  ┌───────────────────────────────────────┐     │
│  │  /jwce/index.html                     │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  Display                                        │
│  ┌───────────────────────────────────────┐     │
│  │  standalone                    ▼      │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  Theme Color       Background Color             │
│  ┌───────────────┐  ┌───────────────┐         │
│  │  #f6efe9       │  │  #f6efe9       │         │
│  └───────────────┘  └───────────────┘         │
│                                                 │
│  Icon (512x512 PNG)                             │
│  ┌───────────────────────────────────────┐     │
│  │  [  Choose file...  ]  icon-512.png   │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  Maskable Icon (optional)                       │
│  ┌───────────────────────────────────────┐     │
│  │  [  Choose file...  ]  icon-512-maskable.png │
│  └───────────────────────────────────────┘     │
│                                                 │
│              [  Next  ]                         │
│                                                 │
└─────────────────────────────────────────────────┘
```

**填写对照表**：

| 字段 | 填什么 | 说明 |
|------|--------|------|
| **App Name** | `JWCE` | 手机桌面上显示的应用名 |
| **Package ID** | `app.jwce.couple` | Android 唯一标识，建议改成你自己独有的，如 `com.你的名字.jwce` |
| **App Version** | `1.0.0` | 版本号 |
| **App Version Code** | `1` | 内部编号，每次更新 +1 |
| **Start URL** | `/jwce/index.html` | ⚠️ **GitHub Pages 必须带仓库名前缀** |
| **Display** | `standalone` | 已默认，全屏无浏览器栏 |
| **Theme Color** | `#f6efe9` | 状态栏背景色 |
| **Background Color** | `#f6efe9` | 启动屏背景色 |
| **Icon** | 上传 `icons/icon-512.png` | 点击 Choose file 选择 |
| **Maskable Icon** | 上传 `icons/icon-512-maskable.png` | 自适应图标，建议上传 |

> **💡 Package ID 很重要**：一旦确定就不要改，改了等于全新应用，无法覆盖安装。

**图标文件在哪**：就在你下载的 JWCE 项目包里的 `icons/` 文件夹。

---

### Step 6：签名设置

点击 Next 后，会进入签名设置页：

```
┌─────────────────────────────────────────────────┐
│  🔐 Signing options                             │
│                                                 │
│  How would you like to sign your app?           │
│                                                 │
│  ┌───────────────────────────────────────┐     │
│  │  🔑 New                               │     │
│  │  Generate a new signing key            │     │
│  │  ✅ Recommended for first-time users   │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  ┌───────────────────────────────────────┐     │
│  │  📂 Upload your own                   │     │
│  │  Use an existing keystore file         │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  ┌───────────────────────────────────────┐     │
│  │  🚫 No signing                        │     │
│  │  Skip signing (testing only)           │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│              [  Next  ]                         │
│                                                 │
└─────────────────────────────────────────────────┘
```

**三个选项怎么选**：

| 选项 | 适合谁 | 能否上架 Play Store |
|------|--------|---------------------|
| **New** | ✅ **首次使用，推荐** | ✅ 可以 |
| **No signing** | 只想本地测试 | ❌ 不可以 |
| **Upload your own** | 已有 keystore 的老手 | ✅ 可以 |

**如果你只是想自己用**：选 **No signing**，跳过签名，直接下一步。

**如果你想以后上架应用商店**：选 **New**，PWABuilder 会帮你生成密钥。

> **⚠️ 选了 New 的话**：下载的 ZIP 里会有一个 `signing.keystore` 文件，**务必保存好**，以后每次更新都要用它。

---

### Step 7：开始构建

确认所有配置无误后，点击 **"Download"** 或 **"Build"** 按钮。

**你会看到构建进度**：

```
┌─────────────────────────────────────────────────┐
│  ⏳ Building your Android app...                │
│                                                 │
│  [████████████████████░░░░░░]  75%             │
│                                                 │
│  Generating TWA project...                      │
│  Configuring Gradle build...                     │
│  Compiling APK...                               │
│                                                 │
│  ⏱️ 预计还需 15 秒                              │
└─────────────────────────────────────────────────┘
```

等待 **30~60 秒**，构建完成后浏览器会自动下载一个 ZIP 文件，文件名类似 `jwce-android.zip`。

---

### Step 8：解压并找到 APK

1. 解压下载的 ZIP 文件
2. 进入解压后的文件夹

**你看到的文件结构应该是这样**：

```
jwce-android/                          ← 解压后的文件夹
├── app-release-signed.apk             ← ✅ 这个就是安装包！
├── signing.keystore                   ← 🔑 签名密钥（选了 New 才有）
├── signing-key-info.txt               ← 📄 密钥信息
├── assetlinks.json                    ← 🔗 数字资产链接
├── build.gradle                       ← 📄 构建配置
├── AndroidManifest.xml                ← 📄 清单文件
├── src/                               ← 📁 源码目录
└── ...                                ← 其他文件
```

**你要的只有这一个文件**：

```
app-release-signed.apk
```

> 如果选了 No signing，文件名可能是 `app-release-unsigned.apk`，一样的。

---

### Step 9：安装到手机

#### 方式 A：传到手机安装（最简单）

1. 把 APK 文件传到手机（**任选一种方式**）：
   - 微信「文件传输助手」
   - 数据线复制
   - 网盘（百度网盘、阿里云盘等）
   - 邮件附件

2. 在手机上打开这个 APK 文件

3. 如果提示 **"不允许安装未知来源应用"**，按以下路径开启：

   | 手机品牌 | 开启路径 |
   |----------|----------|
   | **原生 Android** | 设置 → 应用和通知 → 高级 → 特殊应用权限 → 安装未知应用 → 选择当前来源（如"文件管理"）→ 允许 |
   | **小米 / Redmi** | 设置 → 隐私保护 → 特殊权限设置 → 安装未知应用 → 选择来源 → 允许 |
   | **华为 / 荣耀** | 设置 → 安全 → 更多安全设置 → 安装未知应用 → 选择来源 → 允许 |
   | **OPPO / vivo** | 设置 → 隐私 → 特殊权限 → 安装未知应用 → 选择来源 → 允许 |
   | **三星** | 设置 → 生物识别和安全 → 安装未知应用 → 选择来源 → 允许 |

4. 点击 **"安装"** → 等待完成 → 点击 **"打开"**

#### 方式 B：ADB 安装（开发者）

```bash
# 手机开启 USB 调试，用数据线连接电脑
adb install app-release-signed.apk
```

---

## ✅ 安装后验收清单

安装完成后，打开应用，逐项验证：

| # | 检查项 | 怎么看 | 预期结果 |
|---|--------|--------|----------|
| 1 | 桌面图标 | 回到手机桌面看图标 | 显示 **JW** 标识图标 |
| 2 | 启动屏 | 打开应用的瞬间 | 显示 **#f6efe9 米色**背景，短暂显示后进入应用 |
| 3 | 全屏模式 | 看顶部有没有浏览器栏 | **无**浏览器地址栏，像原生 App |
| 4 | 首页加载 | 进入应用后 | 正常显示日期、导航栏 |
| 5 | 功能可用 | 点几个按钮试试 | 能添加任务、记录心情 |
| 6 | 数据保留 | 添加一条记录后关闭应用，再打开 | 数据还在 |
| 7 | 离线可用 | 关闭 WiFi/数据，重新打开应用 | 仍能正常使用 |

**全部通过 → 恭喜，APK 构建成功！** 🎉

---

## 🔄 后续更新流程

每次修改代码后，需要重新生成 APK：

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│   ① 修改代码   ② git push   ③ 等 Pages 更新   ④ 重新打包   │
│                                                          │
│   ┌────────┐   ┌────────┐   ┌──────────┐   ┌────────┐  │
│   │ 改 HTML │──▶│ 推送   │──▶│ 等 1 分钟 │──▶│ PWABuilder │  │
│   │ 改 CSS  │   │ GitHub │   │ CDN 刷新 │   │ 重新生成  │  │
│   └────────┘   └────────┘   └──────────┘   └────────┘  │
│                                      │                  │
│                                      ▼                  │
│                            ┌────────────────┐          │
│                            │ 安装到手机验证   │          │
│                            └────────────────┘          │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

**详细步骤**：

1. 修改代码 → `git push` 到 GitHub
2. GitHub Pages 自动更新（约 1 分钟）
3. 打开 PWABuilder → 输入同一地址 → Start
4. **Package ID 保持不变**（和上次一样！）
5. **App Version Code +1**（如从 1 改为 2）
6. **使用同一个签名密钥**（上传上次保存的 `signing.keystore`）
7. 重新下载 APK
8. 手机上卸载旧版，安装新版

> **⚠️ 三个不能变**：Package ID、签名密钥、应用名称。变了就无法覆盖安装。

---

## 🔐 签名密钥管理

### 保存密钥

下载的 ZIP 中包含 `signing.keystore` 和 `signing-key-info.txt`，务必：

1. **复制到两个不同位置**（如电脑 + U 盘）
2. **记录密码和别名**（写在纸上或密码管理器）
3. **不要上传到 GitHub**（`.gitignore` 已排除）

### 密钥信息记录模板

建议创建一个 `my-keystore-info.txt`（**仅本地保存，不上传**）：

```
应用名: JWCE
包名: app.jwce.couple
密钥库文件: signing.keystore
密钥库密码: xxxxxxxx
密钥别名: xxxxxxxx
密钥密码: xxxxxxxx
生成日期: 2026-xx-xx
```

### 密钥丢失怎么办

- 无法更新已安装的 APK（签名不一致）
- 只能生成新密钥，用户需卸载旧版再装新版
- **建议一开始就备份好**

---

## ❓ 常见问题

### Q1：PWABuilder 检测失败，"Manifest not found"

**原因**：URL 路径不正确。

**对照检查**：

| ❌ 错误填法 | ✅ 正确填法 |
|-------------|-------------|
| `github.com/用户名/jwce` | `https://用户名.github.io/jwce/` |
| `https://github.com/用户名/jwce/tree/main` | `https://用户名.github.io/jwce/` |
| `https://用户名.github.io/jwce` | `https://用户名.github.io/jwce/`（补 `/`） |
| `http://用户名.github.io/jwce/` | `https://用户名.github.io/jwce/`（改 https） |

**还不行？** 强制刷新 PWABuilder 页面：`Ctrl + F5`（Mac 为 `Cmd + Shift + R`），重新输入 URL。

---

### Q2：检测提示图标相关错误

这个项目已经通过 PWABuilder 的图标检测（10 个图标、type 字段、maskable 全部合规）。**如果还报错，99% 是 URL 问题，不是代码问题。**

**自检方法**：浏览器直接打开图标地址，看能不能显示：

```
https://用户名.github.io/jwce/icons/icon-512.png
```

- 能显示 → URL 问题，回到 Q1 检查
- 不能显示 → 文件没上传成功，检查 icons 文件夹

---

### Q3：APK 安装后白屏

**原因**：TWA 无法加载在线 PWA（网络问题或 URL 配置错误）。

**排查步骤**：

1. 确认手机有网
2. 在手机浏览器打开 `https://用户名.github.io/jwce/`，确认能访问
3. 检查 PWABuilder 配置的 **Start URL** 是否正确（GitHub Pages 需带 `/jwce/` 前缀）
4. 如果经常离线使用，建议改用 Capacitor 方案（见对比表）

---

### Q4：APK 打开后显示浏览器地址栏

**原因**：Digital Asset Links 未配置。

**解决**：
- 将 ZIP 中的 `assetlinks.json` 部署到 `https://用户名.github.io/.well-known/assetlinks.json`
- GitHub Pages 部署方式：在仓库根目录创建 `.well-known/assetlinks.json` 文件，内容复制自 ZIP 中的同名文件

> **如果只是自己用**，地址栏不影响功能，可以暂时忽略。

---

### Q5：安装提示 "应用未安装"

**原因**：签名冲突。

**解决**：
1. 先卸载手机上已有的 JWCE
2. 确保每次构建使用**同一个签名密钥**
3. 如果换了电脑，记得把之前保存的 `signing.keystore` 上传到 PWABuilder

---

### Q6：下载的 ZIP 里没有 APK？

**原因**：构建可能失败了。

**解决**：
1. 检查浏览器是否拦截了下载
2. 重新点击 Build，等待完整构建过程
3. 如果持续失败，尝试换浏览器（Chrome 优先）

---

### Q7：想同时支持 Android 和 iOS？

| 平台 | 方案 |
|------|------|
| **Android** | 本文档的 PWABuilder 方案，生成 APK |
| **iOS** | iPhone 用户在 Safari 中打开 PWA 地址 → 分享 → 添加到主屏幕，无需 APK |

---

## 📊 三种 APK 方案对比

| 维度 | PWABuilder（本文） | Capacitor | Bubblewrap CLI |
|------|-------------------|-----------|----------------|
| 难度 | ⭐ 最简单 | ⭐⭐⭐ 需装 Android Studio | ⭐⭐ 需命令行 |
| 时间 | 10~15 分钟 | 30~60 分钟 | 20~30 分钟 |
| 需要域名 | ✅ 必需 | ❌ 不需要 | ✅ 必需 |
| 离线启动 | ⚠️ 依赖 SW 缓存 | ✅ 完全内置 | ⚠️ 依赖 SW 缓存 |
| 上架 Play Store | ✅ 支持 AAB | ✅ 支持 AAB | ✅ 支持 AAB |
| 推荐场景 | 快速侧载测试 | 需要纯离线 | 喜欢命令行的开发者 |

---

## 💡 快速回顾

```
① 打开 PWABuilder.com
        │
        ▼
② 输入 https://用户名.github.io/jwce/
        │
        ▼
③ 点击 Start，等待检测（全部 🟢）
        │
        ▼
④ 点击 Build My PWA → 选择 Android
        │
        ▼
⑤ 填写参数（App Name=JWCE, Start URL=/jwce/index.html）
        │
        ▼
⑥ 选择签名方式（No signing / New）
        │
        ▼
⑦ 点击 Download，等待构建
        │
        ▼
⑧ 解压 ZIP，找到 app-release-signed.apk
        │
        ▼
⑨ 传到手机，允许未知来源，安装
        │
        ▼
🎉 完成！
```

---

## 🔗 相关文档

- **DEPLOY_GUIDE.md** — GitHub Pages 部署指南（本文档的前置步骤）
- **RELEASE_GUIDE.md** — GitHub 开源发布完整流程
- **README.md** — 项目主文档
- [PWABuilder 官方文档](https://docs.pwabuilder.com/)
- [PWABuilder Android 打包文档](https://docs.pwabuilder.com/#/builder/android?id=packaging)
