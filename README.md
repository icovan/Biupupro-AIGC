# 必有谱 AIGC 系统（Biupu Pro）

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![PHP](https://img.shields.io/badge/PHP-8.1+-777BB4?logo=php)](https://www.php.net/)
[![ThinkPHP](https://img.shields.io/badge/ThinkPHP-8.x-green.svg)](https://www.thinkphp.cn/)
[![Vue](https://img.shields.io/badge/Vue-3.x-4FC08D?logo=vue.js)](https://v3.cn.vuejs.org/)

基于 [MofAdmin](https://www.modoer.cn/) 的 AI 创作与打谱系统，对接国内主流 AI 平台，支持 AI 识谱、AI打谱；内置 **iDapu** 模块，支持 AlphaTex 乐谱编辑与 AI 智能打谱、激活码授权等能力。

<img width="1912" height="922" alt="image" src="https://github.com/user-attachments/assets/acb9d51f-a050-4635-9988-76b4d49c5db8" />

---

## 一、系统说明

**必有谱 AIGC 系统** 是一套前后端分离的 Web 应用：

- **后端**：基于 PHP 8.1+ 与 ThinkPHP 8，采用模块化设计，模块可热插拔。
- **管理端**：Vue 3（非构建模式）+ Element Plus，用于系统配置、用户与权限、AI 通道、**iDapu 乐谱与激活码**等管理。
- **用户端**：Vue 3 + Element Plus + TailwindCSS + Vite 构建，支持 PC 与移动端自适应；集成 **AlphaTab** 乐谱渲染、**iDapu/AlphaTex** 文本编辑与 **AI 打谱**。

系统在通用 AIGC 能力（AI识谱）之上，通过 **iDapu** 模块提供：

- 乐谱的创建、编辑、保存（iDapu 文本 / AlphaTex 文本）。
- 使用 AI 根据自然语言、歌词或和弦描述生成 AlphaTex 乐谱。
- 激活码的生成、发放与用户端激活，便于商业化或授权管理。

---

## 二、功能特色

### 通用 AIGC

- 对接国内各大 AI 平台，支持多通道配置与切换。
- AI 识谱、打谱。
- 后台常用组件封装，以 PHP 为主即可完成管理界面开发，降低前端参与度、提升开发效率。

### iDapu 乐谱与 AI 打谱

- **双输入模式**：支持 **iDapu 文本** 与 **AlphaTex 文本** 编辑，并可由后台配置默认曲谱类型与默认内容。
- **AlphaTab 渲染**：用户端集成 AlphaTab，实时渲染六线谱/简谱/五线谱。
- **AI 打谱**：根据自然语言、歌词或和弦进行，由 AI 生成符合 AlphaTex 语法的乐谱文本，可直接渲染。
- **可配置提示词**：后台可配置系统提示词、打谱语法说明与示例片段，以提升生成质量与格式一致性。

### 授权与商业化

- **激活码管理**：后台支持激活码的创建、批量生成、编辑、删除与授权操作。
- **用户端激活**：用户登录后可查看「我的激活码」、使用激活码激活，与现有用户体系打通。
- **配置灵活**：可配置激活码有效期、AI 打谱所用通道、打谱模式、默认曲谱等。

### 技术架构

- 前后端分离，RESTful API，JWT 鉴权。
- 模块化与热插拔，便于扩展与二次开发。
- 用户端 WEB 自适应，一套代码兼顾 PC 与 Mobile。

---

## 三、技术栈

| 类别     | 技术 |
|----------|------|
| 后端     | PHP 8.1+、ThinkPHP 8、MofAdmin |
| 前端（管理端） | Vue 3、Element Plus（非构建模式） |
| 前端（用户端） | Vue 3、Element Plus、TailwindCSS、Vite、AlphaTab、KaTeX、Markdown-it |
| 数据与缓存 | MySQL 5.7+、Redis 5.0+ |
| 其他     | Composer、Nginx/Apache |

---

## 四、环境要求

- **PHP** 8.1+
- **MySQL** 5.7+
- **Redis** 5.0+
- **Nginx** 或 **Apache**
- **Composer** 2.0+
- **Node.js** 与 **npm**（用于构建用户端）

**PHP 扩展**：`redis`、`zip`、`iconv`、`fileinfo`、`json`。

若使用宝塔等面板，请在 PHP 设置中解禁：`putenv`、`proc_open`。

---

## 五、安装说明

### 5.1 克隆代码

```bash
# GitHub
git clone https://github.com/zaokework/biupu-pro.git

# 或 Gitee
git clone https://gitee.com/zaokework/biupu-pro.git

cd biupu-pro
```

### 5.2 安装后端依赖

在项目根目录执行（国内建议使用 [阿里云](https://developer.aliyun.com/composer) 或 [腾讯云](https://mirrors.tencent.com/help/composer.html) Composer 镜像）：

```bash
composer install
```

### 5.3 配置环境

1. 复制环境示例文件并重命名为 `.env`：

   ```bash
   cp .env.sample .env
   ```

2. 编辑 `.env`，配置：
   - **数据库**：`[DATABASE]` 下 `HOSTNAME`、`DATABASE`、`USERNAME`、`PASSWORD`、`HOSTPORT`、`prefix`
   - **JWT**：`[JWT]` 下 `KEY`（必填，用于登录与接口鉴权）
   - 若使用 Redis，请根据框架约定在应用配置中启用并填写 Redis 连接

### 5.4 安装系统

在项目根目录执行：

```bash
php think mof:install
```

按提示完成安装并创建管理员账号。

### 5.5 Web 服务器

- 将网站根目录指向项目的 **`public`** 目录。
- 确保 Nginx/Apache 已配置好 PHP 与 URL 重写（ThinkPHP 单入口）。

### 5.6 访问管理端

管理端为 Vue 非构建模式，无需额外构建。

- 访问：`https://你的域名/admin/index.html`
- 使用安装时创建的管理员账号登录。
- 在后台可配置 AI 通道、iDapu 打谱与激活码等相关选项。

### 5.7 构建与部署用户端

1. 进入用户端目录并安装依赖：

   ```bash
   cd front-end/web
   npm install
   ```

2. 复制前端环境文件并配置接口地址：

   ```bash
   cp .env.development .env.production
   ```

   编辑 `.env.production`，将 `VITE_API_URL` 改为你的后端域名，例如：

   ```env
   VITE_API_URL=https://你的系统安装域名
   ```

3. 构建：

   ```bash
   npm run build
   ```

4. 将 `front-end/web/dist` 目录部署到你的 Web 服务器（可与后端同域或独立域名），通过浏览器访问即可使用用户端（含乐谱编辑与 AI 打谱）。

更详细的安装步骤、常见问题与目录结构说明见 [安装文档](docs/傻瓜式部署.md)。

---

## 六、演示

- **前台**：https://pu.biunow.cn/

---

## 七、目录结构概览

```
biupu-pro/
├── app/                    # 应用层
├── module/                 # 业务模块（含 idapu、user、ai 等）
│   └── idapu/              # iDapu 乐谱与 AI 打谱、激活码
├── front-end/
│   └── web/                # 用户端 Vue 项目
├── public/                 # Web 根目录
├── .env.sample             # 环境变量示例
├── composer.json
└── README.md
```

---

## 八、开发与使用文档

- **软件架构**：[软件架构说明](docs/系统架构.md)（总体架构、后端模块与路由、前端双端、数据流与模块依赖）
- **使用说明**：[用户与管理员使用说明](用户手册.md)（前端打谱/有谱/个人中心、后台功能与常见流程）
- 开发文档：待完善  
- iDapu 认证与接口说明：见 `module/idapu/docs/`  

---

## 九、鸣谢

感谢以下项目与资源：

- [ThinkPHP](https://www.thinkphp.cn/)
- [Element Plus](https://element-plus.org/)
- [Vue 3](https://v3.cn.vuejs.org/)
- [Vite](https://cn.vitejs.dev/)
- [TailwindCSS](https://tailwindcss.com/)
- [AlphaTab](https://www.alphatab.net/)
- [MofAdmin](https://www.modoer.cn/)

---

## 十、版权与许可证

本项目遵循 **Apache-2.0** 开源协议发布，可免费试用。  
其中所包含的第三方源码与二进制文件的版权信息见各自标注。

**Copyright © 2018-2026 MouferStudio (https://pu.biunow.cn)**  
All rights reserved.

---

## 联系与反馈

如有疑问或建议，可通过 [官网](https://pu.biunow.cn/) 或项目 Issues 联系。

![微信](docs/ScreenShot_2026-03-11_000543_180.png)

