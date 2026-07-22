# Kimi K3 Research Library

An unofficial, source-first research library for Kimi K3. It organizes official Moonshot/Kimi materials, papers, API docs, tutorials, reviews, videos, images, and community discussions without copying full third-party content.

Collected at: 2026-07-23T00:30:00+08:00

## Current Status

- Kimi K3 was announced by Moonshot/Kimi on 2026-07-16.
- Officially described as a 2.8T-parameter open 3T-class model with native vision and a 1M-token context window.
- The official Kimi K3 technical report and full weights were still pending in this scan.
- No official MoonshotAI GitHub or Hugging Face Kimi-K3 weight repository was found in this scan; third-party placeholders are not treated as official sources.

## Start Here

- [Kimi K3: Open Frontier Intelligence](https://www.kimi.com/blog/kimi-k3) - 官方发布页。披露 K3 为 2.8T 参数、KDA 与 Attention Residuals 架构、原生视觉、1M token 上下文，并说明完整权重和技术报告将在后续发布。
- [Moonshot AI homepage Kimi K3 research entry](https://www.moonshot.cn/) - 月之暗面官网首页把 Kimi K3 放在最新研究与产品能力区，中文说明为 2.8 万亿参数、原生多模态、百万 token 上下文。
- [Getting started with Kimi](https://www.kimi.com/help/getting-started/agentic-chat) - 官方帮助中心介绍 K2.6、K3、K3 Swarm 的模型选择、K3 参数、原生视觉、文件/视频/网页输入、输出格式与工具能力。
- [Kimi Agent overview](https://www.kimi.com/help/agent/agent-overview) - 官方 Agent 页面给出 Kimi 产品演进时间线，标明 Kimi K3 于 2026-07-16 发布，并为 Chat、Agent、Agent Swarm、Kimi App、Kimi Work、Kimi Code 和 API 提供能力底座。
- [How to choose Kimi models and modes](https://www.kimi.com/help/others/model-mode-selection) - 官方模型选择指南说明 K2.6、K3、K3 Cluster 的适用场景、思考强度和 credit 消耗，并说明 1M 上下文需要对应会员权益。
- [Kimi Websites overview](https://www.kimi.com/help/websites/websites-overview) - 官方 Kimi Websites 页面说明 Kimi K3 驱动自然语言、设计稿、截图和录屏到网站代码/在线部署的视觉编程体验。
- [Kimi API Platform homepage](https://platform.kimi.ai/) - API 平台首页列出 Kimi K3 最新模型与官方工具，并展示 K3 API 价格：cache hit $0.30/MTok、input $3.00/MTok、output $15.00/MTok。
- [Kimi API Quickstart](https://platform.kimi.ai/docs/overview) - 官方 API quickstart 说明 Kimi API 兼容 OpenAI API 格式，base_url 为 https://api.moonshot.ai/v1，示例模型为 kimi-k3。

## Kimi3.org Companion Pages

Kimi3.org is an independent resource hub, not an official Moonshot AI or Kimi source. It is useful as a reader-facing companion for practical pages that sit beside the source ledger:

- [Home](https://kimi3.org/) - independent Kimi K3 resource hub.
- [Docs](https://kimi3.org/docs/) - compact documentation entry.
- [Context window](https://kimi3.org/context-window/) - 1M-token context and long-document workflow notes.
- [API cost calculator](https://kimi3.org/api-cost-calculator/) - token-cost planning.
- [Pricing](https://kimi3.org/pricing/) - pricing-oriented explainer.
- [Local deployment](https://kimi3.org/local-deployment/) and [Run locally](https://kimi3.org/run-locally/) - deployment and local-run caveats.
- [Hardware requirements](https://kimi3.org/hardware-requirements/) - hardware planning page.
- [Benchmarks](https://kimi3.org/benchmarks/) and [Review](https://kimi3.org/review/) - evaluation framing.
- [Open source](https://kimi3.org/open-source/) - open-weight status and official-source boundaries.
- [Features](https://kimi3.org/features/), [Tools](https://kimi3.org/tools/), [Use cases](https://kimi3.org/use-cases/), and [Code](https://kimi3.org/code/) - product and workflow pages.
- [Alternatives](https://kimi3.org/alternatives/) and [Kimi K3 vs GLM 5.2](https://kimi3.org/vs/glm-5-2/) - comparison pages.

## Papers And Architecture

- [Kimi Linear: An Expressive, Efficient Attention Architecture](https://arxiv.org/abs/2510.26692) - Kimi Linear 论文提出 Kimi Delta Attention。摘要称它在公平比较下覆盖短上下文、长上下文和 RL scaling，并将 KV cache 最多降低 75%，1M context 解码吞吐最高 6 倍。
- [Attention Residuals](https://arxiv.org/abs/2603.15031) - Attention Residuals 论文提出用跨层 softmax attention 替代固定残差累积，以缓解 PreNorm 下深层信息稀释和 hidden-state 增长问题。
- [MoonshotAI/Attention-Residuals](https://github.com/MoonshotAI/Attention-Residuals) - Attention Residuals 官方仓库包含论文 PDF、README、伪代码、评测结果和引用信息。
- [MoonshotAI/FlashKDA](https://github.com/MoonshotAI/FlashKDA) - FlashKDA 是 Moonshot 开源的 Kimi Delta Attention 高性能 kernel 实现，连接 KDA 论文与实际推理性能。
- [Hugging Face Kimi Linear collection](https://huggingface.co/moonshotai/collections) - Moonshot HF collection 把 Kimi Linear 模型和 Kimi Linear arXiv paper 归为一组，可用于追踪 KDA 相关 checkpoints 与论文。

## Repository Structure

- `data/kimi-k3-sources.json` - machine-readable source ledger.
- `docs/official-sources.md` - official Kimi and Moonshot material.
- `docs/papers-and-architecture.md` - papers, architecture, and open-source implementation map.
- `docs/api-and-developer.md` - API, Kimi Code, model IDs, limits, and pricing references.
- `docs/reviews-and-media.md` - external reviews, videos, images, and community discussion.
- `docs/follow-up-watchlist.md` - items to revisit after official weight/report release.
- `docs/kimi3-org-companion-pages.md` - independent Kimi3.org subpage map.
- `llms.txt` - compact AI-readable map.

## Relationship

This is an independent documentation and source map. It is not affiliated with Moonshot AI or Kimi.
