# hoppscotchGreenWeb

> 基于 Hoppscotch 的独立前端改版项目

<div align="center">

**轻量级 API 开发工具的前端实现**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README_EN.md) | **中文**

</div>

---

## 📖 项目简介

hoppscotchGreenWeb 是一个基于 [Hoppscotch](https://github.com/hoppscotch/hoppscotch) 的独立前端改版项目。我们专注于提供简洁、高效的 API 测试和开发体验，保留了 Hoppscotch 核心的请求发送、响应查看、集合管理等前端功能，同时针对本地化使用场景进行了优化和裁剪。

### 核心特性

- ⚡ **快速请求**：支持 GET、POST、PUT、DELETE 等多种 HTTP 方法
- 🎨 **主题定制**：明暗主题切换，多种配色方案
- 📁 **集合管理**：无限层级的请求组织和分类
- 🔧 **环境变量**：灵活的环境变量管理和复用
- 🌐 **多协议支持**：HTTP、WebSocket、GraphQL、SSE、Socket.IO、MQTT
- 📝 **脚本扩展**：支持预请求脚本和测试脚本
- 💾 **本地存储**：数据完全存储在本地，保护隐私

---

## 🔗 与 Hoppscotch 的关系

本项目是 [Hoppscotch](https://github.com/hoppscotch/hoppscotch) 的一个 **fork / 独立改版**，具有以下特点：

- ❌ **非官方项目**：不属于 Hoppscotch 官方项目体系
- ❌ **无官方背书**：未获得 Hoppscotch 官方的赞助、认证、背书或维护
- ✅ **保留原始许可**：继承原项目的 MIT License，保留所有版权声明
- ✅ **感谢原作者**：衷心感谢 Hoppscotch 团队及所有贡献者的开源工作

**官方项目地址**：https://github.com/hoppscotch/hoppscotch  
**官方文档**：https://docs.hoppscotch.io

---

## ✨ 主要改动

相较于原版 Hoppscotch，本项目进行了以下核心调整：

### 1. 仅保留前端部分

聚焦于纯前端能力的实现，包含以下核心包：

- `hoppscotch-selfhost-web`：自托管 Web 版主应用
- `hoppscotch-common`：共享组件和核心逻辑
- `hoppscotch-data`：数据模型和序列化
- `hoppscotch-kernel`：内核模块
- 其他前端相关依赖包

移除了后端服务（`hoppscotch-backend`）、管理后台（`hoppscotch-sh-admin`）等服务器端组件。

### 2. 移除 / 禁用登录相关能力

为简化部署和保护用户隐私，我们对以下功能进行了裁剪：

- ❌ **账号系统**：移除了 GitHub、Google、Microsoft、邮箱等登录方式
- ❌ **云端同步**：禁用了跨设备的数据同步功能
- ❌ **团队协作**：移除了 Teams、Workspaces 等多人协作特性
- ❌ **SSO 集成**：不再支持企业级单点登录

所有数据均存储在浏览器本地（LocalStorage / IndexedDB），完全由用户掌控。

### 3. 修改自托管和构建配置

针对本地开发和简单部署场景优化了构建流程：

- 简化了环境变量配置，仅需关注 `VITE_` 前缀的前端变量
- 提供了更轻量的开发服务器启动方式
- 优化了生产构建的资源体积和加载性能
- 适配静态文件服务器部署（如 Nginx、Caddy）

---

## 🚀 安装与运行

### 前置要求

在开始之前，请确保你的系统已安装：

- **Node.js** >= 22.x
- **pnpm** >= 10.32.1

> 💡 推荐使用 [fnm](https://github.com/Schniz/fnm) 或 [nvm](https://github.com/nvm-sh/nvm) 管理 Node.js 版本

### 快速开始

#### 1. 克隆仓库

```bash
git clone <your-repo-url>
cd hoppscotchGreenWeb
```

#### 2. 安装依赖

```bash
pnpm install
```

首次安装会自动生成 GraphQL 类型定义，可能需要几分钟时间。

#### 3. 配置环境变量（可选）

```bash
cp .env.example .env
```

编辑 `.env` 文件，根据需要配置 `VITE_` 开头的环境变量。对于大多数本地使用场景，可以使用默认配置。

#### 4. 启动开发服务器

**方式一：启动全部前端包**

```bash
pnpm dev
```

**方式二：仅启动自托管 Web 版**

```bash
cd packages/hoppscotch-selfhost-web
pnpm dev
```

开发服务器启动后，访问终端输出的地址（通常是 `http://localhost:3000`）即可使用。

---

## 📦 构建与部署

### 生产构建

#### 构建所有前端包

```bash
pnpm generate
```

这会在各个包的 `dist` 目录下生成优化后的静态文件。

#### 单独构建 selfhost-web

```bash
cd packages/hoppscotch-selfhost-web
pnpm build
```

构建产物位于 `packages/hoppscotch-selfhost-web/dist`。

### 预览构建结果

```bash
pnpm start
```

这会在 `localhost:3000` 启动一个静态文件服务器，用于预览生产构建的效果。

### Docker 部署（可选）

项目提供了完整的 Docker 构建支持：

**使用 docker-compose：**

```bash
docker-compose -f docker-compose.yml up -d
```

**手动构建镜像：**

```bash
docker build -f prod.Dockerfile -t hoppscotch-green-web .
docker run -p 3000:3000 hoppscotch-green-web
```

详细说明请参考：
- [prod.Dockerfile](prod.Dockerfile)：多阶段生产镜像构建
- [docker-compose.yml](docker-compose.yml)：完整的服务编排配置
- [aio_run.mjs](aio_run.mjs)：一体化运行脚本

### 静态文件部署

你也可以将构建产物部署到任意静态文件服务器：

**Nginx 示例配置：**

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/packages/hoppscotch-selfhost-web/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

**Caddy 示例配置：**

```caddy
your-domain.com {
    root * /path/to/packages/hoppscotch-selfhost-web/dist
    file_server
    try_files {path} /index.html
}
```

---

## ⚠️ 免责声明

**请在使用本项目前仔细阅读以下声明：**

### 1. 非官方项目声明

本项目是基于 Hoppscotch 的独立改版 / fork，**不属于 Hoppscotch 官方项目**，也**未获得 Hoppscotch 官方的赞助、背书、认证或维护**。

### 2. 功能差异说明

本项目对原始功能进行了裁剪和调整，**可能移除了登录、账号同步、云端工作区等能力**。因此，本项目的功能表现、配置方式和安全边界可能与官方 Hoppscotch **不一致**。

### 3. 安全警告

⚠️ **请勿在不可信环境中输入敏感凭据、访问令牌、Cookie、生产环境密钥或内部系统地址。**

使用者应自行评估：
- 部署环境的安全性
- 浏览器存储的访问控制
- 网络代理的配置和风险
- 目标 API 的访问权限管理

### 4. 免责条款

本项目按 **"现状"（AS IS）** 提供，**不提供任何明示或暗示的担保**，包括但不限于适销性、特定用途适用性和非侵权性的担保。

**因使用本项目造成的以下损失，项目维护者不承担任何责任：**
- 数据泄露或丢失
- API 请求误发或滥用
- 配置错误导致的服务异常
- 直接或间接的经济损失
- 其他任何形式的损害

### 5. 版权与许可

本项目包含来源于 Hoppscotch 的代码。原项目的**版权、商标、名称、Logo 及相关权益归其原权利人所有**。

本项目保留适用的原始版权声明和许可证信息（MIT License）。使用本项目时，请遵守原项目的许可条款。

---

## 📜 开源协议与鸣谢

### 许可证

本项目采用 **MIT License**，详见 [LICENSE](LICENSE) 文件。

```
MIT License

Copyright (c) 2022

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

### 致谢

- 🙏 **Hoppscotch 团队**：感谢你们创造了如此优秀的开源 API 开发工具
- 🙏 **所有贡献者**：感谢每一位为 Hoppscotch 项目做出贡献的开发者
- 🙏 **开源社区**：感谢所有支撑本项目的基础设施和依赖库的维护者

本项目站在巨人的肩膀上，我们致力于在尊重原创的基础上提供有价值的改进。

---

## 🔒 安全提示

### 最佳实践建议

1. **本地优先**：尽量在本地环境或可信的内网中使用
2. **定期备份**：导出重要的集合和环境变量配置
3. **谨慎分享**：不要随意分享包含敏感信息的请求配置
4. **更新依赖**：定期执行 `pnpm update` 获取安全补丁

### 报告安全问题

如发现安全漏洞，请参考原项目的 [SECURITY.md](SECURITY.md) 了解报告流程。

对于本项目特有的安全问题，请通过 Issue 或私信方式联系维护者。

### 了解更多

- [Hoppscotch 官方安全策略](https://github.com/hoppscotch/hoppscotch/blob/main/SECURITY.md)
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
- [Web 应用安全最佳实践](https://developer.mozilla.org/zh-CN/docs/Web/Security)

---

## 📚 相关资源

- **官方文档**：https://docs.hoppscotch.io（参考原版功能说明）
- **原项目仓库**：https://github.com/hoppscotch/hoppscotch
- **问题反馈**：在本项目仓库提交 Issues
- **贡献指南**：参见 [CONTRIBUTING.md](CONTRIBUTING.md)

---

<div align="center">

**Made with ❤️ by hoppscotchGreenWeb Contributors**

基于 Hoppscotch · 独立改版 · 本地优先

</div>
