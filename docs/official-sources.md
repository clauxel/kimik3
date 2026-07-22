# Official Sources

Official Kimi, Moonshot, API, product, repository, and model-hosting sources.

Collected at: 2026-07-23T00:30:00+08:00

## Kimi K3: Open Frontier Intelligence

- URL: https://www.kimi.com/blog/kimi-k3
- Type: official technical blog
- Priority: P0
- Status: verified
- Language: en
- Published: 2026-07-16

官方发布页。披露 K3 为 2.8T 参数、KDA 与 Attention Residuals 架构、原生视觉、1M token 上下文，并说明完整权重和技术报告将在后续发布。

Key points:
- K3 是 Kimi 当前最强模型，面向长程编码、知识工作和推理。
- 官方承认整体能力仍落后最强闭源模型，但在其评测套件中达前沿水平。
- 完整权重计划最晚 2026-07-27 发布，技术报告随架构/训练/评测细节后续公开。

Follow-up: 2026-07-27 后复核权重、license、模型卡与技术报告链接。


## Moonshot AI homepage Kimi K3 research entry

- URL: https://www.moonshot.cn/
- Type: official company site
- Priority: P0
- Status: verified
- Language: zh
- Published: 2026-07-16 listing

月之暗面官网首页把 Kimi K3 放在最新研究与产品能力区，中文说明为 2.8 万亿参数、原生多模态、百万 token 上下文。

Key points:
- 官网中文口径与 Kimi 英文博客一致。
- 官方产品入口包括 Kimi、API、Kimi Code、Kimi Work 等。


## Getting started with Kimi

- URL: https://www.kimi.com/help/getting-started/agentic-chat
- Type: official help center
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方帮助中心介绍 K2.6、K3、K3 Swarm 的模型选择、K3 参数、原生视觉、文件/视频/网页输入、输出格式与工具能力。

Key points:
- K3 支持图片、视频、文档、URL 等多模态输入。
- K3 可端到端输出 docx、pptx、xlsx、pdf 等复杂产物。
- K3 与 K3 Swarm 按会员 credit 计费。


## Kimi Agent overview

- URL: https://www.kimi.com/help/agent/agent-overview
- Type: official help center
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方 Agent 页面给出 Kimi 产品演进时间线，标明 Kimi K3 于 2026-07-16 发布，并为 Chat、Agent、Agent Swarm、Kimi App、Kimi Work、Kimi Code 和 API 提供能力底座。

Key points:
- Agent Swarm 可并行使用大量工具/子任务，适合大规模搜索和批处理。
- K3 是 Kimi Agent、网站、文档、表格、PPT、深度研究等产品线的能力核心。


## How to choose Kimi models and modes

- URL: https://www.kimi.com/help/others/model-mode-selection
- Type: official help center
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方模型选择指南说明 K2.6、K3、K3 Cluster 的适用场景、思考强度和 credit 消耗，并说明 1M 上下文需要对应会员权益。

Key points:
- K3 适合复杂会话、文档/PPT/表格、多步骤任务。
- K3 Cluster 面向大规模搜索、批处理和超长文写作。
- K2.6 单轮约 128K token；K3 可提供 1M token 上下文。


## Kimi Websites overview

- URL: https://www.kimi.com/help/websites/websites-overview
- Type: official help center
- Priority: P1
- Status: verified
- Language: en
- Published: date needs review

官方 Kimi Websites 页面说明 Kimi K3 驱动自然语言、设计稿、截图和录屏到网站代码/在线部署的视觉编程体验。

Key points:
- K3 的视觉和代码能力被用于网站生成与多轮修改。
- 适合收集网站生成教程、Vibe Coding 评测和视觉代码案例。


## Kimi API Platform homepage

- URL: https://platform.kimi.ai/
- Type: official API platform
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

API 平台首页列出 Kimi K3 最新模型与官方工具，并展示 K3 API 价格：cache hit $0.30/MTok、input $3.00/MTok、output $15.00/MTok。

Key points:
- K3 是 API 平台 flagship model，支持 1M-token context。
- 价格需要按官方平台当前页面复核，税费另算。


## Kimi API Quickstart

- URL: https://platform.kimi.ai/docs/overview
- Type: official API docs
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方 API quickstart 说明 Kimi API 兼容 OpenAI API 格式，base_url 为 https://api.moonshot.ai/v1，示例模型为 kimi-k3。

Key points:
- 示例支持 Python、curl、Node.js。
- K3 使用顶层 reasoning_effort 字段，支持 low/high/max，默认 max。
- K3、K2.7 Code、K2.6 都支持文本、图像和视频输入。


## Kimi K3 API guide

- URL: https://platform.kimi.ai/docs/guide/kimi-k3-quickstart
- Type: official API docs
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方 K3 API 专页说明 K3 的 capability、调用示例、thinking effort、streaming、vision input、structured output、tool choice、dynamic tools、1M context 和重要限制。

Key points:
- K3 always thinks；不能关闭 chain-of-thought，只能调低 reasoning_effort。
- max_completion_tokens 默认 131072，可设到 1048576。
- temperature、top_p 等参数固定；vision input 不支持公共图片 URL，需 base64 或 ms:// file-id。
- 官方提示 web_search 正在更新，短期不建议用于生产。


## Flagship Model Kimi K3 Pricing

- URL: https://platform.kimi.ai/docs/pricing/chat-k3
- Type: official API pricing
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方 K3 定价页说明计费单位、税费说明和模型描述；价格表在平台首页可见，需以官方页面当前状态为准。

Key points:
- K3 pay-as-you-go 不按上下文长度分层计费。
- 输入、输出与 cache hit 分开计价。


## Kimi Code model configuration

- URL: https://www.kimi.com/code/docs/en/kimi-code/models.html
- Type: official Kimi Code docs
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

Kimi Code 官方模型配置文档列出 K3 的 Model ID 为 k3，上下文最高 1M，reasoning effort 为 low/high/max，并说明第三方工具接入 Base URL。

Key points:
- 官方 Kimi Code CLI 可用 /model 切换。
- OpenAI compatible coding endpoint 为 https://api.kimi.com/coding/v1。
- Anthropic compatible coding endpoint 为 https://api.kimi.com/coding/。
- 第三方工具若要用满 1M 上下文，需要手动配置 1048576。


## Kimi Code What’s New

- URL: https://www.kimi.com/code/docs/en/kimi-code/whats-new.html
- Type: official Kimi Code docs
- Priority: P1
- Status: verified
- Language: en
- Published: date needs review

Kimi Code 更新记录标出 2026-07-16 Kimi K3 模型发布与 2026-07-17 v0.27.0 更新。

Key points:
- K3 已接入 Kimi Code。
- v0.27.0 支持 API key 用户自动刷新模型列表。


## MoonshotAI GitHub organization

- URL: https://github.com/MoonshotAI
- Type: official GitHub organization
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

官方 GitHub 组织列出 Kimi Code、Kimi CLI、Kimi-K2、Kimi-K2.5、Attention-Residuals、FlashKDA 等开源项目；当前扫描未看到官方 Kimi-K3 权重仓库。

Key points:
- K3 权重仓库需要 2026-07-27 后复核。
- 可先从 Kimi-K2/K2.5、Kimi Linear、Attention Residuals、FlashKDA 追踪架构脉络。

Follow-up: 复核 https://github.com/MoonshotAI/Kimi-K3 是否出现。


## Moonshot AI Hugging Face organization

- URL: https://huggingface.co/moonshotai
- Type: official Hugging Face organization
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

Moonshot Hugging Face 组织当前列出 Kimi K2.7 Code、K2.6、K2.5、Kimi Linear、Kimi Audio 等模型与论文集合；当前扫描未看到 moonshotai/Kimi-K3。

Key points:
- HF 组织是权重发布后最需要复核的位置之一。
- 不要把第三方占位页误认为官方发布。

Follow-up: 复核 https://huggingface.co/moonshotai/Kimi-K3 是否出现。


## MoonshotAI/Attention-Residuals

- URL: https://github.com/MoonshotAI/Attention-Residuals
- Type: official GitHub repo
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

Attention Residuals 官方仓库包含论文 PDF、README、伪代码、评测结果和引用信息。

Key points:
- 适合放入论文材料与架构解释页。
- README 给出 Block AttnRes 的 PyTorch 风格伪代码和 scaling law 结果摘要。


## MoonshotAI/FlashKDA

- URL: https://github.com/MoonshotAI/FlashKDA
- Type: official GitHub repo
- Priority: P0
- Status: verified
- Language: en
- Published: date needs review

FlashKDA 是 Moonshot 开源的 Kimi Delta Attention 高性能 kernel 实现，连接 KDA 论文与实际推理性能。

Key points:
- 用于收集 KDA 的工程实现与部署前置资料。
- 后续 K3 权重开放后要复核其是否被 vLLM、FlashKDA 或其他 inference 栈支持。


