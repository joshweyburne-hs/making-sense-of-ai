# Supervised Fine-Tuning (SFT)

Supervised Fine-Tuning is the process of training a pre-trained language model on curated instruction-response pairs to teach it specific behaviors, formats, and capabilities. It is the "monkey see, monkey do" phase where the model learns by imitating high-quality examples of desired output.

## How It Works

SFT takes a pre-trained model that can predict text but has no concept of being helpful and teaches it to follow instructions. The training data consists of paired examples: an instruction or prompt, and the ideal response. The model processes the instruction, generates a response, and its parameters are adjusted to increase the probability of producing the demonstrated response. The loss function is negative log-likelihood: minimize the difference between the model's predicted token probabilities and the actual tokens in the target response.

The power of SFT is in the data quality, not quantity. Research from LIMA (Less Is More for Alignment) showed that just 1,000 carefully selected examples could produce a model competitive with those trained on 50,000+ examples. Each example must demonstrate not just the correct answer but the correct style, format, reasoning process, and tone. This is why expert-authored examples consistently outperform crowd-sourced ones.

Full fine-tuning updates every parameter in the model. For a 70B model, this requires substantial GPU memory and compute, as you need to store the model, gradients, and optimizer states simultaneously. This typically demands multiple high-end GPUs.

LoRA (Low-Rank Adaptation) revolutionized fine-tuning accessibility. Instead of updating all parameters, LoRA freezes the original weights and injects small trainable matrices (adapters) into each layer. These adapters typically represent 0.1-1% of the total parameter count. QLoRA extends this by quantizing the frozen base model to 4-bit precision, reducing memory requirements further. A 70B model that would require 8x A100 GPUs for full fine-tuning can be QLoRA fine-tuned on a single A100.

SFT is powerful for teaching format, style, and behavioral patterns. It reliably teaches a model to respond in JSON, follow a specific persona, cite sources in a particular format, or maintain a specific communication style. However, SFT is limited to imitation. It can teach a model to mimic good behavior but cannot teach it to reason about why one response is better than another. For that, you need reinforcement learning.

## Medical Analogy

SFT is the attending physician phase of residency. The resident watches the attending interact with patients, observes their diagnostic approach, mirrors their communication style, and follows their treatment protocols. It is learning by example. The resident becomes competent by imitating excellent practice. But imitation has limits. To develop independent judgment, to choose between two plausible treatment plans, the resident needs experience making decisions and receiving feedback on outcomes. That is where reinforcement learning begins.

## Why It Matters for Enterprise AI

SFT is the most practical entry point for most enterprises building AI capability. The barrier is not compute or complexity; it is having the right examples. This is where the 42% of abandoned initiatives often fail: organizations try to fine-tune on noisy, inconsistent data instead of investing in curated examples that reflect their best practices. Your codified craftsmanship, captured as high-quality instruction-response pairs, is the ground truth that SFT needs. A hundred excellent examples from your top performers can teach a model your institutional voice, your decision frameworks, your quality standards. That is tribal knowledge made scalable. The strategic moat is not in the fine-tuning technique; it is in the quality of examples that only your people can create.

## Key Technical Details

- Loss function: negative log-likelihood (cross-entropy) on target tokens
- Dataset size: 1K-100K examples; quality matters far more than quantity
- Full fine-tuning: updates all parameters; requires multi-GPU setups for large models
- LoRA: adds ~0.1-1% trainable parameters via low-rank adapter matrices
- QLoRA: combines LoRA with 4-bit quantized base model; single-GPU fine-tuning
- Training time: hours to days depending on model size and dataset
- Risk: catastrophic forgetting if fine-tuned too aggressively on narrow data
- LIMA paper: 1,000 high-quality examples competitive with 50K+ crowd-sourced

## Related Terms

- [Post-training](post-training.md)
- [Reinforcement Learning](reinforcement-learning.md)
- [Transfer Learning](transfer-learning.md)
- [RLHF & Alignment Techniques](rlhf-and-alignment-techniques.md)
- [Weights & Parameters](weights-and-parameters.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
