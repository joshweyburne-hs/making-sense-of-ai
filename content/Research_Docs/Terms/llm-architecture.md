# LLM Architecture

Large Language Model architecture refers to the layered processing systems that transform raw text into meaningful predictions. Modern LLMs are predominantly decoder-only Transformers, processing information through dozens to hundreds of sequential layers that progressively refine understanding from surface-level patterns to abstract reasoning.

## How It Works

The foundational architecture was introduced in the 2017 paper "Attention Is All You Need" by Vaswani et al. at Google Brain. The original Transformer used an encoder-decoder structure designed for translation tasks, but the field quickly discovered that decoder-only architectures (GPT-style) were more effective for general text generation. This single architectural bet now underpins virtually every frontier model: GPT-4, Claude, Gemini, Llama, and DeepSeek.

Information flows through the model in a forward pass. Raw text enters as tokens, gets converted into numerical embeddings, then passes through a stack of identical layers. Each layer contains two core components: a self-attention mechanism and a feed-forward network. The self-attention mechanism determines which parts of the input are relevant to each other. The feed-forward network transforms those relationships into richer representations.

Lower layers tend to capture syntax and surface patterns. Middle layers encode semantic relationships and factual associations. Upper layers handle abstract reasoning and task-specific behavior. This progressive refinement is why scaling depth (more layers) has proven so effective. A 70-billion-parameter model might have 80 layers, while a 405-billion-parameter model could have 126.

The architecture is autoregressive, meaning it generates one token at a time, with each new token conditioned on all previous tokens. This sequential generation is why inference speed is a constraint, and why techniques like speculative decoding and parallel drafting have become active research areas.

Residual connections and layer normalization keep gradients flowing during training, enabling the extreme depth that modern models require. Without these architectural details, training a model with hundreds of layers would be numerically unstable.

## Medical Analogy

Think of LLM architecture as the structure of the human brain's language processing centers. Just as Broca's area handles production while Wernicke's area handles comprehension, each layer in a Transformer handles different levels of linguistic abstraction. The architecture itself does not contain knowledge; it is the scaffolding that makes learning possible.

## Why It Matters for Enterprise AI

Understanding architecture matters because it determines what is possible and what is not. When your organization evaluates AI solutions, architecture choices dictate latency, cost, and capability ceilings. The $252B invested in AI has produced remarkable architectures, but architecture alone does not solve your problems. Over 80% of AI investments show no meaningful EBIT impact because organizations deploy powerful architectures without feeding them the institutional knowledge that makes outputs actionable. The architecture is the engine. Your domain expertise, workflow understanding, and tribal knowledge are the fuel. Without that fuel, you have an expensive machine idling in the parking lot. Your strategic moat is not the architecture; it is the codified craftsmanship your people bring to every decision.

## Key Technical Details

- Decoder-only Transformers dominate: GPT, Llama, Claude, Gemini, DeepSeek all use this pattern
- Layer counts range from 32 (7B models) to 126+ (405B+ models)
- Each layer contains multi-head self-attention + feed-forward network + normalization
- Residual (skip) connections prevent vanishing gradients in deep networks
- Autoregressive generation: one token at a time, left-to-right
- The original 2017 Transformer had 65M parameters; modern models exceed 1 trillion
- KV-cache stores previously computed attention states to avoid redundant computation during generation

## Related Terms

- [Transformers & Self-Attention](transformers-and-attention.md)
- [Weights & Parameters](weights-and-parameters.md)
- [Tokenization](tokenization.md)
- [Pre-training](pre-training.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
