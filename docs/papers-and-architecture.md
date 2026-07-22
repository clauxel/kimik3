# Papers And Architecture

Papers and official implementation repositories that explain the architecture behind Kimi K3 claims.

Collected at: 2026-07-23T00:30:00+08:00

## Kimi Linear: An Expressive, Efficient Attention Architecture

- URL: https://arxiv.org/abs/2510.26692
- Type: arXiv paper
- Priority: P0
- Status: verified
- Language: en
- Published: 2025-10-30

Kimi Linear 论文提出 Kimi Delta Attention。摘要称它在公平比较下覆盖短上下文、长上下文和 RL scaling，并将 KV cache 最多降低 75%，1M context 解码吞吐最高 6 倍。

Key points:
- KDA 是 K3 官方博客明确提到的关键架构来源。
- 论文提供 KDA kernel、vLLM 实现和模型 checkpoints 的研究路线。


## Attention Residuals

- URL: https://arxiv.org/abs/2603.15031
- Type: arXiv paper
- Priority: P0
- Status: verified
- Language: en
- Published: 2026-03-16

Attention Residuals 论文提出用跨层 softmax attention 替代固定残差累积，以缓解 PreNorm 下深层信息稀释和 hidden-state 增长问题。

Key points:
- AttnRes 是 K3 官方架构说明的另一核心组件。
- Block AttnRes 通过分块降低大规模训练的内存与通信开销。


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


## Hugging Face Kimi Linear collection

- URL: https://huggingface.co/moonshotai/collections
- Type: official HF collection
- Priority: P1
- Status: verified
- Language: en
- Published: date needs review

Moonshot HF collection 把 Kimi Linear 模型和 Kimi Linear arXiv paper 归为一组，可用于追踪 KDA 相关 checkpoints 与论文。

Key points:
- Kimi Linear 48B-A3B 是 KDA 与长上下文效率材料的关键背景。


