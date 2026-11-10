# SecurePass · macOS 本地加密账号密码管家

一款运行在 macOS 上的账号密码管理软件，采用 Apple 简约风格、蓝白配色、黑色字体，自带内置加密数据库，所有敏感字段均以密文形式本地存储，不上传任何服务器。

作者 ID：**©️JohnJHZhang**

版本号：**v2.0.0**
---

## ✨ 功能特性

### 主页（密码库）
统一管理每条账号信息，字段包含：
- 平台 / 网站
- 账号
- 密码（含**密码强度检测**，弱 / 中 / 强 / 极强可视化进度条）
- 邮箱
- 手机号码
- 备注

支持搜索、按算法筛选、一键复制密码、查看详情、编辑、删除。

### 二级界面 · 随机密码生成器
- 三种密码类型：**随机 / 容易记住 / # PIN 码**
- 自定义密码**长度**（滑块）
- 自定义字符集：大写字母、小写字母、**数字**、**特殊符号**开关
- **实时显示**生成的密码与强度
- **复制密码**按钮、**刷新密码**按钮

### 安全
- **锁定功能**：首次使用时设置解锁密码；可随时手动锁定（标题栏按钮或快捷键 `Cmd+L`）
- 解锁密码通过 **PBKDF2-SHA256（12 万次迭代）** 派生主密钥，主密钥仅存在于内存
- 可修改解锁密码（自动用新密钥重新加密全部数据）
- 支持加密备份的导出 / 导入

---

## 🔐 加密算法

所有数据库内容均可选择以下加密方式，**默认优先使用 AES-256**：

| 算法 | 说明 | 密钥长度 |
|------|------|----------|
| **AES-256**（默认） | AES-256-GCM，国际主流、带完整性校验 | 256 bit |
| **国密 SM4** | 中国商用密码分组标准 GB/T 32907，SM4-CBC | 128 bit |
| **DES** | 经典 64 位分组算法，DES-CBC，仅供兼容场景 | 64 bit |
| **SM1** | 见下方说明 | — |

> **关于 SM1：** SM1 是国家商用密码分组算法，其**算法细节不公开，只能通过专用加密芯片（硬件）调用**，在纯软件环境中无法实现。因此当用户选择 SM1 时，软件会**安全回退到同为国密标准的 SM4**，并在界面中明确标注（`SM1→SM4`）。这是业界处理 SM1 的通行做法。

SM4 与 DES 的实现均已通过官方标准测试向量（KAT）验证：
- SM4：GB/T 32907 标准示例 `681edf34d206965e86b3e94f536e4246` ✅
- DES：FIPS 标准示例 `85e813540f0ab405` ✅

---

## 🚀 运行方式

### 方式一：作为 macOS 原生应用运行（推荐）
需要 Node.js 环境：

```bash
cd SecurePass
npm install          # 安装 Electron
npm start            # 启动应用
```

### 打包为 .app / .dmg 安装包
```bash
npm run dist         # 产物在 dist/ 目录
```

### 方式二：浏览器中直接打开
双击 `index.html` 即可在浏览器中体验全部功能（数据存于浏览器本地存储）。

> 注：加密依赖浏览器原生 Web Crypto（AES-256），请使用 Safari / Chrome 等现代浏览器。

---

## 📁 文件结构

```
SecurePass/
├── index.html      # 界面结构
├── styles.css      # Apple 简约风样式（蓝白配色）
├── crypto.js       # 加密引擎：AES-256 / SM4 / DES + 强度检测 + 密码生成
├── app.js          # 主程序逻辑：数据库 / 锁定 / CRUD / 生成器
├── main.js         # Electron 主进程（macOS 原生窗口）
├── package.json    # 应用打包配置
└── assets/
    ├── logo.svg    # 软件 Logo（盾牌钥匙）
    └── icon.png    # 应用图标
```

---

## 🔒 隐私说明
- 所有数据仅保存在本机（localStorage / 应用沙盒），**不联网、不上传**。
- 忘记解锁密码将无法恢复数据，请妥善保管。
- 导出的备份文件中内容仍为密文，但请勿随意外传。

---

© 2026 SecurePass  ·  作者： ©️JohnJHZhang

版本号：v2.0.0

<img width="1092" height="788" alt="01" src="https://github.com/user-attachments/assets/66a87bff-20dc-4420-abf3-a0ebb827fac7" />
<img width="978" height="676" alt="02" src="https://github.com/user-attachments/assets/ceed1a6a-b1f9-4188-a3cc-5409be62b464" />
<img width="974" height="675" alt="03" src="https://github.com/user-attachments/assets/6dddba3c-6fdc-4bef-9d3c-3eecc6496c26" />
<img width="1136" height="808" alt="04" src="https://github.com/user-attachments/assets/404f8cd3-6010-4f00-8cab-f581e57a2f91" />
<img width="1130" height="805" alt="05" src="https://github.com/user-attachments/assets/a325c1ca-4eae-497b-a686-c5fa22abdd21" />
<img width="1252" height="921" alt="06" src="https://github.com/user-attachments/assets/3c407b40-5bfa-4061-836b-1ff5ddc07193" />
<img width="1252" height="921" alt="07" src="https://github.com/user-attachments/assets/e5500665-e1cc-48cd-b890-76fe88ca19b6" />
<img width="1252" height="921" alt="08" src="https://github.com/user-attachments/assets/a1eb6283-407a-41ce-a836-b5e916fadfce" />
<img width="1252" height="921" alt="09" src="https://github.com/user-attachments/assets/5be8931f-ac49-47ed-9731-a2062cc22abc" />
<img width="1313" height="1139" alt="10" src="https://github.com/user-attachments/assets/b50005dc-6952-4e03-84a0-ad004a4a7a44" />
