# hoppscotchGreenWeb

> A standalone frontend fork of Hoppscotch

<div align="center">

**Lightweight API Development Tool - Frontend Implementation**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**English** | [中文](README.md)

</div>

---

## 📖 Project Overview

hoppscotchGreenWeb is an independent frontend fork based on [Hoppscotch](https://github.com/hoppscotch/hoppscotch). We focus on providing a clean and efficient API testing and development experience, retaining core frontend features such as request sending, response viewing, and collection management, while optimizing for local usage scenarios.

### Core Features

- ⚡ **Fast Requests**: Support for GET, POST, PUT, DELETE, and other HTTP methods
- 🎨 **Theme Customization**: Light/dark theme switching with multiple color schemes
- 📁 **Collection Management**: Unlimited hierarchical request organization
- 🔧 **Environment Variables**: Flexible environment variable management and reuse
- 🌐 **Multi-Protocol Support**: HTTP, WebSocket, GraphQL, SSE, Socket.IO, MQTT
- 📝 **Script Extensions**: Pre-request scripts and test scripts support
- 💾 **Local Storage**: All data stored locally for privacy protection

---

## 🔗 Relationship with Hoppscotch

This project is a **fork / independent modification** of [Hoppscotch](https://github.com/hoppscotch/hoppscotch) with the following characteristics:

- ❌ **Not Official**: Not part of the official Hoppscotch project ecosystem
- ❌ **No Endorsement**: Not sponsored, certified, endorsed, or maintained by Hoppscotch officially
- ✅ **Original License Retained**: Inherits the original MIT License with all copyright notices preserved
- ✅ **Credits to Original Authors**: Sincere thanks to the Hoppscotch team and all contributors for their open-source work

**Official Project**: https://github.com/hoppscotch/hoppscotch  
**Official Documentation**: https://docs.hoppscotch.io

---

## ✨ Key Changes

Compared to the original Hoppscotch, this project has made the following core adjustments:

### 1. Frontend Only

Focused on pure frontend capabilities, including these core packages:

- `hoppscotch-selfhost-web`: Self-hosted web main application
- `hoppscotch-common`: Shared components and core logic
- `hoppscotch-data`: Data models and serialization
- `hoppscotch-kernel`: Kernel modules
- Other frontend-related dependency packages

Removed backend services (`hoppscotch-backend`), admin dashboard (`hoppscotch-sh-admin`), and other server-side components.

### 2. Removed / Disabled Login Capabilities

To simplify deployment and protect user privacy, we have trimmed the following features:

- ❌ **Account System**: Removed login methods including GitHub, Google, Microsoft, and email
- ❌ **Cloud Sync**: Disabled cross-device data synchronization
- ❌ **Team Collaboration**: Removed Teams, Workspaces, and other multi-user collaboration features
- ❌ **SSO Integration**: No longer supports enterprise single sign-on

All data is stored in browser local storage (LocalStorage / IndexedDB), fully controlled by users.

### 3. Modified Self-Hosting and Build Configuration

Optimized build processes for local development and simple deployment scenarios:

- Simplified environment variable configuration, focusing only on `VITE_` prefixed frontend variables
- Provided lighter development server startup methods
- Optimized production build asset size and loading performance
- Adapted for static file server deployment (e.g., Nginx, Caddy)

---

## 🚀 Installation & Running

### Prerequisites

Before you begin, ensure your system has:

- **Node.js** >= 22.x
- **pnpm** >= 10.32.1

> 💡 Recommended to use [fnm](https://github.com/Schniz/fnm) or [nvm](https://github.com/nvm-sh/nvm) for Node.js version management

### Quick Start

#### 1. Clone Repository

```bash
git clone <your-repo-url>
cd hoppscotchGreenWeb
```

#### 2. Install Dependencies

```bash
pnpm install
```

First-time installation will automatically generate GraphQL type definitions, which may take a few minutes.

#### 3. Configure Environment Variables (Optional)

```bash
cp .env.example .env
```

Edit the `.env` file to configure `VITE_` prefixed environment variables as needed. For most local usage scenarios, default configuration works fine.

#### 4. Start Development Server

**Option 1: Start all frontend packages**

```bash
pnpm dev
```

**Option 2: Start self-hosted web version only**

```bash
cd packages/hoppscotch-selfhost-web
pnpm dev
```

After the development server starts, visit the URL output in the terminal (usually `http://localhost:3000`) to use the application.

---

## 📦 Build & Deployment

### Production Build

#### Build All Frontend Packages

```bash
pnpm generate
```

This generates optimized static files in the `dist` directory of each package.

#### Build selfhost-web Only

```bash
cd packages/hoppscotch-selfhost-web
pnpm build
```

Build artifacts are located in `packages/hoppscotch-selfhost-web/dist`.

### Preview Build Results

```bash
pnpm start
```

This starts a static file server at `localhost:3000` to preview the production build.

### Docker Deployment (Optional)

The project provides complete Docker build support:

**Using docker-compose:**

```bash
docker-compose -f docker-compose.yml up -d
```

**Manual image build:**

```bash
docker build -f prod.Dockerfile -t hoppscotch-green-web .
docker run -p 3000:3000 hoppscotch-green-web
```

For detailed instructions, please refer to:
- [prod.Dockerfile](prod.Dockerfile): Multi-stage production image build
- [docker-compose.yml](docker-compose.yml): Complete service orchestration configuration
- [aio_run.mjs](aio_run.mjs): All-in-one runtime script

### Static File Deployment

You can also deploy build artifacts to any static file server:

**Nginx Example Configuration:**

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

**Caddy Example Configuration:**

```caddy
your-domain.com {
    root * /path/to/packages/hoppscotch-selfhost-web/dist
    file_server
    try_files {path} /index.html
}
```

---

## ⚠️ Disclaimer

**Please read the following disclaimer carefully before using this project:**

### 1. Non-Official Project Statement

This project is an independent fork/modification based on Hoppscotch. It **does not belong to the official Hoppscotch project** and has **not received sponsorship, endorsement, certification, or maintenance from Hoppscotch officially**.

### 2. Feature Differences

This project has trimmed and adjusted original functionalities, **possibly removing login, account synchronization, cloud workspace, and other capabilities**. Therefore, the feature behavior, configuration methods, and security boundaries of this project may be **inconsistent** with official Hoppscotch.

### 3. Security Warning

⚠️ **DO NOT enter sensitive credentials, access tokens, cookies, production environment keys, or internal system addresses in untrusted environments.**

Users should independently evaluate:
- Security of the deployment environment
- Access control of browser storage
- Configuration and risks of network proxies
- Access permission management of target APIs

### 4. Liability Disclaimer

This project is provided **"AS IS"** without **any express or implied warranties**, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement.

**Project maintainers shall not be held liable for any losses caused by using this project, including but not limited to:**
- Data leakage or loss
- Misuse or abuse of API requests
- Service anomalies caused by configuration errors
- Direct or indirect economic losses
- Any other forms of damage

### 5. Copyright and Licensing

This project contains code sourced from Hoppscotch. The **copyrights, trademarks, names, logos, and related rights of the original project belong to their respective owners**.

This project retains applicable original copyright notices and license information (MIT License). When using this project, please comply with the licensing terms of the original project.

---

## 📜 Open Source License & Acknowledgments

### License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2022

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

### Acknowledgments

- 🙏 **Hoppscotch Team**: Thank you for creating such an excellent open-source API development tool
- 🙏 **All Contributors**: Thanks to every developer who has contributed to the Hoppscotch project
- 🙏 **Open Source Community**: Gratitude to all maintainers of the infrastructure and dependencies supporting this project

This project stands on the shoulders of giants. We are committed to providing valuable improvements while respecting the original work.

---

## 🔒 Security Tips

### Best Practice Recommendations

1. **Local First**: Use in local environments or trusted intranets whenever possible
2. **Regular Backups**: Export important collections and environment variable configurations
3. **Share Carefully**: Do not casually share request configurations containing sensitive information
4. **Update Dependencies**: Regularly run `pnpm update` to obtain security patches

### Reporting Security Issues

If you discover security vulnerabilities, please refer to the original project's [SECURITY.md](SECURITY.md) for reporting procedures.

For security issues specific to this project, please contact maintainers through Issues or private messages.

### Learn More

- [Hoppscotch Official Security Policy](https://github.com/hoppscotch/hoppscotch/blob/main/SECURITY.md)
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
- [Web Application Security Best Practices](https://developer.mozilla.org/en-US/docs/Web/Security)

---

## 📚 Related Resources

- **Official Documentation**: https://docs.hoppscotch.io (Reference for original feature descriptions)
- **Original Repository**: https://github.com/hoppscotch/hoppscotch
- **Issue Reporting**: Submit Issues in this project repository
- **Contributing Guide**: See [CONTRIBUTING.md](CONTRIBUTING.md)

---

<div align="center">

**Made with ❤️ by hoppscotchGreenWeb Contributors**

Based on Hoppscotch · Independent Fork · Local First

</div>
