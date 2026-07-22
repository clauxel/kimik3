# API And Developer Notes

API quickstarts, pricing, Kimi Code model IDs, reasoning effort, context limits, and tool behavior.

Collected at: 2026-07-23T00:30:00+08:00

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


