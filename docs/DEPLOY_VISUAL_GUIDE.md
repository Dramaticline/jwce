# 📸 GitHub Pages 部署图文指南（独立版）

> **本文档独立成文**，不依赖其他指南，照着做即可把 JWCE 部署到公网。
> 适合：零服务器运维经验、没有域名、不想花钱的用户。
> 预计耗时：**10~20 分钟**（含首次部署等待时间）。

---

## 📋 开始前：准备两样东西

| # | 需要什么 | 怎么获取 |
|---|----------|----------|
| 1 | **GitHub 账号** | [github.com/join](https://github.com/join) 免费注册 |
| 2 | **JWCE 项目文件** | 就是你手上的这个压缩包，解压后得到 `jwce-pwa-release/` 文件夹 |

**不需要准备**：服务器、域名、SSL 证书、信用卡。

---

## 🚀 完整图文步骤

### Step 1：创建 GitHub 仓库

#### 1.1 打开新建仓库页面

浏览器访问 **[github.com/new](https://github.com/new)**，登录后会看到这个表单：

```
┌─────────────────────────────────────────────────┐
│  Create a new repository                         │
│                                                 │
│  ─────────────────────────────────────────────  │
│                                                 │
│  Repository name  *                              │
│  ┌───────────────────────────────────────┐     │
│  │  jwce                                  │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  Description  (optional)                         │
│  ┌───────────────────────────────────────┐     │
│  │  JWCE - 本地优先的情侣日常记录 PWA      │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  ☑️ Public                                      │
│  ⬜️ Private                                     │
│                                                 │
│  ⬜️ Add a README file                           │
│  ⬜️ Add .gitignore                             │
│  ⬜️ Choose a license                            │
│                                                 │
│              [  Create repository  ]            │
│                                                 │
└─────────────────────────────────────────────────┘
```

#### 1.2 按下面要求填写

| 字段 | 填什么 | ⚠️ 注意事项 |
|------|--------|-------------|
| **Repository name** | `jwce` | 必须小写，建议就叫 jwce |
| **Description** | 选填 | 可以写 `JWCE - 本地优先的情侣日常记录 PWA` |
| **Public / Private** | ☑️ **Public** | ⚠️ **必须选 Public**，Private 无法用免费 Pages |
| **Add a README** | ⬜️ **不要勾** | 压缩包里已有 README.md |
| **Add .gitignore** | ⬜️ **不要勾** | 压缩包里已有 |
| **Choose a license** | ⬜️ **不要勾** | 压缩包里已有 LICENSE |

#### 1.3 点击创建

点击绿色按钮 **Create repository**。

**创建成功后**，你会看到一个**空仓库页面**，地址栏类似：

```
https://github.com/你的用户名/jwce
```

> **把这个地址记下来**，后面要用。

---

### Step 2：上传项目文件

> **这一步最容易出错**，请仔细看。

#### 2.1 进入上传页面

在刚创建的空仓库页面，找到并点击 **"uploading an existing file"** 链接。

也可以直接在地址栏末尾加 `/upload`：

```
https://github.com/你的用户名/jwce/upload
```

#### 2.2 选择要上传的文件

**⚠️ 关键：不要上传外层文件夹，只上传文件夹里面的内容。**

❌ **错误做法**：把整个 `jwce-pwa-release` 文件夹拖进去
✅ **正确做法**：打开 `jwce-pwa-release` 文件夹，选中里面的**所有内容**拖进去

**操作演示**：

```
你的电脑文件管理器：

📁 Downloads/
   📁 jwce-pwa-release/          ← 打开这个文件夹
      │
      ├── 📄 index.html          ┐
      ├── 📄 manifest.json       │
      ├── 📄 sw.js               │
      ├── 📄 offline.html        │  ← 选中这些
      ├── 📄 LICENSE             │     拖到浏览器
      ├── 📄 README.md           │
      ├── 📄 CONTRIBUTING.md     │
      ├── 📄 PRIVACY.md          │
      ├── 📄 SECURITY.md         │
      ├── 📄 .gitignore          │
      ├── 📁 icons/              │
      ├── 📁 docs/               │
      └── 📁 .github/            ┘
```

**拖进浏览器后，上传区应该显示这些文件**：

```
┌─────────────────────────────────────────────────┐
│  📂 Drag files here to add them to your repository
│                                                 │
│  ✅ index.html                        3.2 KB   │
│  ✅ manifest.json                    1.8 KB   │
│  ✅ sw.js                            4.1 KB   │
│  ✅ offline.html                     1.5 KB   │
│  ✅ LICENSE                          1.1 KB   │
│  ✅ README.md                        5.2 KB   │
│  ✅ CONTRIBUTING.md                  2.3 KB   │
│  ✅ PRIVACY.md                       1.4 KB   │
│  ✅ SECURITY.md                      2.1 KB   │
│  ✅ .gitignore                         185 B   │
│  ✅ icons/  (10 files)                        │
│  ✅ docs/  (3 files)                          │
│  ✅ .github/  (4 files)                       │
│                                                 │
│  📊 25 files, 467 KB total                    │
│                                                 │
└─────────────────────────────────────────────────┘
```

#### 2.3 提交上传

滚动到页面底部，填写提交信息：

| 字段 | 填什么 |
|------|--------|
| **Commit message** | `feat: 初始化 JWCE PWA 项目` |
| **Description** | 留空即可 |
| **分支** | 保持默认的 `main` |

点击绿色按钮 **Commit changes**。

**等待上传完成**（文件较多时约 30 秒~2 分钟）。

---

### Step 3：开启 GitHub Pages

#### 3.1 进入 Pages 设置

1. 进入仓库页面
2. 点击顶部导航的 **Settings**（齿轮图标）
3. 在左侧菜单找到并点击 **Pages**

#### 3.2 配置 Pages

你会看到类似这样的页面：

```
┌─────────────────────────────────────────────────┐
│  ⚙️ Pages Settings                              │
│                                                 │
│  Build and deployment                            │
│                                                 │
│  Source                                          │
│  ┌───────────────────────────────────────┐     │
│  │  Deploy from a branch          ▼      │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  ┌─────────────────┐  ┌─────────────────┐     │
│  │  Branch: main   │  │  Folder: / (root)│     │
│  └─────────────────┘  └─────────────────┘     │
│                                                 │
│  ☑️ Enforce HTTPS                               │
│                                                 │
│              [  Save  ]                         │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│  🟡 GitHub Pages is currently being built...    │
│     We'll let you know when it's ready.         │
│                                                 │
└─────────────────────────────────────────────────┘
```

**按下面配置**：

| 配置项 | 选择 |
|--------|------|
| **Source** | ✅ **Deploy from a branch** |
| **Branch** | ✅ **main** |
| **Folder** | ✅ **/ (root)** |
| **Enforce HTTPS** | ✅ 保持勾选（默认就是） |

点击 **Save**。

#### 3.3 等待部署

页面会刷新，顶部出现黄色提示：

> GitHub Pages is currently disabled. We'll let you know when it's ready.

**等 1~3 分钟**，然后**手动刷新页面**。

当看到**绿色提示**时，说明部署成功：

```
┌─────────────────────────────────────────────────┐
│  ✅ Your site is live at                        │
│     https://你的用户名.github.io/jwce/           │
│                                                 │
│  🔗 Visit site                                  │
└─────────────────────────────────────────────────┘
```

> **记好这个地址**，PWABuilder 要用。

---

### Step 4：验证部署成功

**逐项验证，全部通过再进行下一步**。

#### 4.1 验证主页

浏览器打开：

```
https://你的用户名.github.io/jwce/
```

✅ **成功**：看到 JWCE 应用界面
❌ **失败**：显示 404 → 翻到 [常见问题 Q1](#q1访问-pages-地址显示-404)

#### 4.2 验证 manifest

浏览器打开：

```
https://你的用户名.github.io/jwce/manifest.json
```

✅ **成功**：直接显示一段 JSON 文本
❌ **失败**：404 → 文件没上传成功，回 Step 2 检查

#### 4.3 验证图标

浏览器打开：

```
https://你的用户名.github.io/jwce/icons/icon-192.png
```

✅ **成功**：显示一张 192×192 的 JW 图标
❌ **失败**：404 → 检查 icons 文件夹是否上传成功

#### 4.4 验证 Service Worker

1. 打开主页
2. 按 `F12` 打开开发者工具
3. 切到 **Application** 标签 → 左侧 **Service Workers**

**你应该看到**：

```
┌─────────────────────────────────────────────────┐
│  Service Workers                                │
│                                                 │
│  ┌───────────────────────────────────────┐     │
│  │  ✅ sw.js                              │     │
│  │  Status: Activated and running         │     │
│  │  Clients: 1                            │     │
│  └───────────────────────────────────────┘     │
│                                                 │
│  ☑️ Update on reload                            │
│  ☑️ Bypass for network                           │
│                                                 │
└─────────────────────────────────────────────────┘
```

✅ **成功**：sw.js 状态为 **Activated and running**
❌ **失败**：看不到 sw.js → 检查 sw.js 是否上传

#### 4.5 验证离线能力

1. 在开发者工具的 **Network** 标签
2. 把 **No throttling** 改为 **Offline**
3. 刷新页面

✅ **成功**：页面仍能正常显示
❌ **失败**：显示「无法访问此网站」→ SW 未注册成功

**以上 5 项全部通过，部署完成！** 🎉

---

## ❓ 常见问题

### Q1：访问 Pages 地址显示 404

**按以下顺序排查**：

| # | 检查项 | 怎么看 | 解决 |
|---|--------|--------|------|
| 1 | 仓库是否 Public | 仓库页面右侧边栏 | Private 仓库无法用免费 Pages |
| 2 | 文件名是否正确 | 仓库文件列表 | 必须是 `index.html`（注意大小写） |
| 3 | 文件是否在根目录 | 仓库文件列表 | 不能在子文件夹里 |
| 4 | Pages 设置是否正确 | Settings → Pages | Branch=main, Folder=/ (root) |
| 5 | 等待时间 | — | 首次部署有时需要 5 分钟 |

### Q2：上传后仓库里没有文件

**最可能的原因**：上传时只拖了外层文件夹。

**解决**：
1. 在仓库页面点击 **Add file** → **Upload files**
2. **打开** `jwce-pwa-release` 文件夹
3. 选中**里面所有内容**拖进去
4. 填写 Commit message，点 **Commit changes**

### Q3：Pages 设置里看不到 "Deploy from a branch"

**原因**：仓库是空的，没有提交过任何文件。

**解决**：先完成 Step 2 上传文件，再回来设置 Pages。

### Q4：部署成功，但样式全乱了

**原因**：文件路径问题，CSS/JS 没加载。

**解决**：
1. 检查浏览器控制台（F12 → Console）有没有 404 报错
2. 确认所有文件都在仓库**根目录**，不是在子文件夹
3. 强制刷新：`Ctrl + F5`

### Q5：想用自定义域名

如果你有自己的域名（如 `jwce.example.com`）：

1. 在仓库根目录创建文件 `CNAME`，内容为你的域名
2. 在域名服务商处添加 CNAME 记录指向 `你的用户名.github.io`
3. 在 Settings → Pages 里填入自定义域名
4. **好处**：PWABuilder 配置更简单，所有路径统一用 `/` 开头

> 没有域名就跳过，用默认的 `github.io` 地址即可。

---

## 🔄 后续更新流程

改完代码后，推送到 GitHub 即可，**Pages 会自动重新部署**。

### 方式 A：网页拖拽（新手推荐）

1. 在仓库页面点 **Add file** → **Upload files**
2. 只上传**改动过的文件**（不用全部重传）
3. 填写 Commit message，如 `fix: 修复图标显示问题`
4. 点 **Commit changes**
5. 等 1~2 分钟，访问 Pages 地址确认更新

### 方式 B：Git 命令行

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

---

## 📸 关键页面截图位置参考

如果文字描述不够直观，以下是每个步骤你应该看到的页面：

| 步骤 | 页面特征 | 关键元素 |
|------|----------|----------|
| Step 1 | github.com/new | 大表单，Repository name 输入框 |
| Step 2 | 仓库/upload | 虚线框拖拽区 |
| Step 3 | Settings → Pages | Source 下拉框 + Branch 选择 |
| Step 4.1 | 浏览器打开 Pages 地址 | JWCE 应用界面 |
| Step 4.4 | F12 → Application → Service Workers | sw.js 状态 |

---

## 💡 快速回顾

```
① 创建 GitHub 仓库（Public，不要勾任何选项）
        │
        ▼
② 上传文件（打开 jwce-pwa-release，拖入里面所有内容）
        │
        ▼
③ Settings → Pages → Deploy from a branch → main / (root)
        │
        ▼
④ 等 1~3 分钟，看到绿色 "Your site is live at"
        │
        ▼
⑤ 验证 5 项（主页、manifest、图标、SW、离线）
        │
        ▼
🎉 部署完成！地址：https://用户名.github.io/jwce/
```

---

## 🔗 下一步

部署成功后，就可以用 PWABuilder 生成 APK 了：

👉 **[PWABUILDER_VISUAL_GUIDE.md](./PWABUILDER_VISUAL_GUIDE.md)** — PWABuilder 图文操作指南

---

## 📚 相关文档

- **PWABUILDER_VISUAL_GUIDE.md** — PWABuilder 图文操作指南（下一步）
- **RELEASE_GUIDE.md** — GitHub 开源发布完整流程
- **README.md** — 项目主文档
- [GitHub Pages 官方文档](https://docs.github.com/en/pages)
