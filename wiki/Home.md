## 🚀 快速开始

### 一键部署

选择以下任一平台，点击一键部署按钮，即可快速创建自己的 LibreTV 实例：

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fcnrot%2FLibreTV)  
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/cnrot/LibreTV)  
[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/cnrot/LibreTV)

---

## 📖 详细部署

### Vercel

1. Fork 或克隆本仓库到您的 GitHub/GitLab 账户
2. 登录 [Vercel](https://vercel.com/)，点击"New Project"
3. 导入您的仓库，使用默认设置
4. **⚠️ 重要：在"Settings" > "Environment Variables"中添加 `PASSWORD` 变量（必须设置）**
5. 点击"Deploy"

### Docker

```bash
docker run -d \
  --name libretv \
  --restart unless-stopped \
  -p 8899:8080 \
  -e PASSWORD=your_password \
  bestzwei/libretv:latest
```

### Docker Compose

创建 `docker-compose.yml` 文件：

```yaml
services:
  libretv:
    image: bestzwei/libretv:latest
    container_name: libretv
    ports:
      - "8899:8080" # 将内部 8080 端口映射到主机的 8899 端口
    environment:
      - PASSWORD=${PASSWORD:-111111} # 可将 111111 修改为你想要的密码
    restart: unless-stopped
```

启动 LibreTV：

```bash
docker compose up -d
```

访问 `http://localhost:8899` 即可使用。

### 本地开发环境

项目包含后端代理功能，需要支持服务器端功能的环境：

```bash
# 首先，通过复制示例来设置 .env 文件（可选）
cp .env.example .env

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

访问 `http://localhost:8080` 即可使用（端口可在.env文件中通过PORT变量修改）。

> ⚠️ 注意：使用简单静态服务器（如 `python -m http.server` 或 `npx http-server`）时，视频代理功能将不可用，视频无法正常播放。完整功能测试请使用 Node.js 开发服务器。

---

## ⚙️ 配置说明

### 🔐 密码保护

**重要提示**: 为确保安全，所有部署都必须设置 PASSWORD 环境变量，否则用户将看到设置密码的提示。

**设置方法**：
- 在部署平台的环境变量设置中添加 `PASSWORD=your_password`
- 在 Docker 中使用 `-e PASSWORD=your_password`
- 在本地开发中，可以在 `.env` 文件中设置 `PASSWORD=your_password`

### 🔌 API 兼容性

LibreTV 支持标准的苹果 CMS V10 API 格式。添加自定义 API 时需遵循以下格式：

- **搜索接口**: `https://example.com/api.php/provide/vod/?ac=videolist&wd=关键词`
- **详情接口**: `https://example.com/api.php/provide/vod/?ac=detail&ids=视频ID`

**添加 CMS 源步骤**：
1. 在设置面板中选择"自定义接口"
2. 接口地址: `https://example.com/api.php/provide/vod`
3. 保存设置后即可使用

### ⚙️ 环境变量

| 变量名 | 描述 | 默认值 |
|--------|------|--------|
| PASSWORD | 访问密码（必需） | - |
| PORT | 本地开发服务器端口 | 8080 |

### 🛠️ 技术栈

- **前端**: HTML5 + CSS3 + JavaScript (ES6+)
- **样式框架**: Tailwind CSS
- **视频处理**: HLS.js 用于 HLS 流处理
- **播放器**: DPlayer 视频播放器核心
- **服务端**: Cloudflare/Vercel/Netlify Serverless Functions
- **代理**: 服务端 HLS 代理和处理技术
- **存储**: localStorage 本地存储

---

## 🎬 使用指南

### 📱 基本使用步骤

1. **访问 LibreTV**: 打开您部署的 LibreTV 实例
2. **输入密码**: 输入您设置的访问密码
3. **搜索视频**: 在搜索框中输入关键词搜索您想观看的内容
4. **选择源**: 从搜索结果中选择合适的视频源
5. **开始观看**: 点击播放按钮开始观看

### ⌨️ 键盘快捷键

播放器支持以下键盘快捷键：

- **空格键**: 播放/暂停
- **左右箭头**: 快退/快进（通常每次10秒）
- **上下箭头**: 音量增加/减小
- **M 键**: 静音/取消静音
- **F 键**: 全屏/退出全屏
- **Esc 键**: 退出全屏

### 🔍 高级功能

#### 自定义接口

您可以添加自己的视频源：

1. 点击设置图标
2. 选择"自定义接口"
3. 输入符合苹果 CMS V10 API 格式的接口地址
4. 保存设置
5. 返回搜索页面使用新的视频源

#### 多源选择

LibreTV 支持多个视频源，当某个源无法使用时：
1. 尝试切换不同的视频源
2. 检查网络连接
3. 等待一段时间后重试

### 📱 设备兼容性

LibreTV 支持多种设备：
- **桌面端**: Chrome、Firefox、Safari、Edge 等现代浏览器
- **移动端**: iOS Safari、Android Chrome 等移动浏览器
- **平板**: iPad、Android 平板等

---

## 🚨 重要声明与免责声明

### ⚠️ 重要声明

- **本项目仅供学习和个人使用**，为避免版权纠纷，必须设置PASSWORD环境变量
- **请勿将部署的实例用于商业用途或公开服务**
- **如因公开分享导致的任何法律问题，用户需自行承担责任**
- **项目开发者不对用户的使用行为承担任何法律责任**

### 📋 免责声明

LibreTV 仅作为视频搜索工具，不存储、上传或分发任何视频内容。所有视频均来自第三方 API 接口提供的搜索结果。如有侵权内容，请联系相应的内容提供方。

本项目开发者不对使用本项目产生的任何后果负责。使用本项目时，您必须遵守当地的法律法规。

### 📋 使用规范

1. **个人使用**: 仅限个人学习和研究使用
2. **密码保护**: 必须设置访问密码，防止公开访问
3. **合法合规**: 遵守当地法律法规
4. **版权尊重**: 尊重内容创作者的版权
5. **责任自负**: 因使用本项目产生的任何问题由用户自行承担

---

*最后更新时间：2024年*