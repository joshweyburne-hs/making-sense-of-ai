# Weights & Parameters

Weights and parameters are the billions of numerical values inside a large language model that encode everything the model has learned. Every connection between neurons has a weight, and during training, these weights are adjusted incrementally through backpropagation until the model can predict language patterns with high accuracy.

## How It Works

A parameter is a single tunable number in the model. Weights are the subset of parameters that define connection strengths between layers. In practice, the terms are used interchangeably. When we say a model has 70 billion parameters, we mean there are 70 billion individual numbers that were optimized during training to minimize prediction error.

During training, each parameter is adjusted through gradient descent. The model makes a prediction, compares it to the correct answer, computes the error gradient, and nudges each parameter slightly in the direction that reduces error. This happens billions of times across trillions of training tokens. The final parameter values represent compressed statistical patterns extracted from the training corpus.

Parameter counts have scaled dramatically: GPT-2 had 1.5 billion, GPT-3 had 175 billion, and Llama 3.1 reached 405 billion. Google's Switch Transformer crossed 1.76 trillion. But nobody fully understands what individual parameters represent. Unlike a database where you can point to a specific record, model knowledge is distributed across millions of parameters in ways that resist interpretation. This is the "black box" challenge.

Mixture of Experts (MoE) architectures address efficiency by activating only a fraction of parameters per input. A model might have 671 billion total parameters but only activate 37 billion for any given token, routing each input to the most relevant expert sub-networks. DeepSeek-V3 uses this approach, achieving performance competitive with much denser models at lower inference cost.

Quantization reduces parameter precision to improve efficiency. Full-precision training uses 32-bit floating point (FP32), but inference can often run at FP16, INT8, or even INT4 with acceptable quality loss. A 70B model at FP32 requires 280GB of memory; at INT4, it fits in 35GB. This is how open-source models run on consumer hardware. The tradeoff is subtle quality degradation, particularly on tasks requiring precise numerical reasoning.

## Medical Analogy

Parameters are like the synaptic connections in a physician's brain, shaped by years of medical school, residency, and practice. You cannot point to a single synapse and say "that is where the knowledge of cardiac arrhythmia lives." The knowledge is distributed across millions of connections, strengthened through repeated exposure and feedback. Similarly, a model's understanding of language is distributed across billions of parameters that were shaped by trillions of training examples.

## Why It Matters for Enterprise AI

Parameter count is the number everyone fixates on, but it is the wrong metric for enterprise value. Of the $252B invested in AI, a significant portion went to building ever-larger models. Yet over 80% of these investments produced no meaningful EBIT impact. The reason is straightforward: parameters encode general knowledge. Your competitive advantage is not general knowledge. It is the specific, hard-won institutional understanding of your customers, your processes, and your market. A 7B parameter model fine-tuned on your ground truth can outperform a 405B generic model on your tasks. The strategic moat is not parameter count; it is whether those parameters have been shaped by your tribal knowledge. Techniques like LoRA let you add your expertise without retraining from scratch, making codified craftsmanship the most efficient path to AI ROI.

## Key Technical Details

- Parameter counts: 7B (small), 70B (medium), 405B (large), 1.76T (MoE)
- Storage: each FP32 parameter = 4 bytes; 70B model = 280GB at full precision
- Mixture of Experts (MoE): only 10-20% of parameters active per token
- Quantization levels: FP32 → FP16 → INT8 → INT4, each halving memory
- GPTQ and AWQ are popular post-training quantization methods
- Parameters are organized into embedding layers, attention projections, feed-forward layers, and output heads
- Emergent capabilities appear at scale thresholds that are not fully predictable

## Related Terms

- [LLM Architecture](llm-architecture.md)
- [Transformers & Self-Attention](transformers-and-attention.md)
- [Pre-training](pre-training.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
