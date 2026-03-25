# Post-training

Post-training is the phase where a pre-trained language model is transformed from a raw text predictor into a useful, safe, and conversational assistant. It is the clinical rotations phase of model development, where broad foundational knowledge gets shaped into practical, aligned behavior through carefully curated supervision and feedback.

## How It Works

A freshly pre-trained model is powerful but unrefined. It can complete text fluently but has no concept of being helpful, following instructions, refusing harmful requests, or maintaining a coherent conversation. Post-training bridges this gap through a multi-stage alignment pipeline.

The first stage is Supervised Fine-Tuning (SFT), where the model learns to follow instructions by training on thousands to tens of thousands of high-quality instruction-response pairs. These examples demonstrate the desired format, tone, and behavior. Unlike pre-training's trillions of tokens, SFT datasets are small, often 10,000-100,000 examples, but meticulously curated. Quality matters enormously here. A few hundred expert-written examples can outperform tens of thousands of crowd-sourced ones.

The second stage is preference optimization, where the model learns to distinguish better responses from worse ones. This can take several forms: RLHF with PPO (training a reward model and optimizing against it), DPO (directly optimizing on preference pairs), or newer methods like GRPO. Human annotators compare model outputs and indicate which is preferred, and the model learns to produce responses that match human judgment.

The third stage is safety alignment, including red-teaming, constitutional AI principles, and specific training to refuse harmful requests while remaining helpful for legitimate ones. This is where the balance between caution and utility is calibrated.

Post-training is where model personality takes shape. The same base model can become a concise coding assistant, a verbose creative writer, or a cautious medical advisor depending on how post-training is conducted. This is the direct bridge to enterprise fine-tuning: the techniques used by model developers in post-training are the same techniques available to organizations adapting models for their own purposes.

## Medical Analogy

Post-training is clinical rotations. The medical student has passed their foundational exams and now enters the hospital. They work with real patients under supervision. They learn bedside manner, how to communicate diagnoses, when to escalate, and how to handle situations their textbooks never covered. The knowledge was built in pre-training. The professional judgment, the practical skill, the alignment between capability and appropriate behavior, that comes from post-training.

## Why It Matters for Enterprise AI

Post-training is the most accessible lever for enterprise value creation. You cannot afford to pre-train a model (that costs hundreds of millions), but you can absolutely post-train one. The 42% of abandoned AI initiatives often stalled because organizations tried to use generic models without this crucial adaptation step. Post-training is where you inject your institutional knowledge: your customer communication standards, your compliance requirements, your domain-specific decision frameworks. It is the difference between an AI that gives plausible-sounding generic answers and one that operates with the codified craftsmanship of your best people. Your tribal knowledge, encoded through post-training techniques, is what transforms a commodity model into a strategic moat.

## Key Technical Details

- Multi-stage pipeline: SFT → preference optimization → safety alignment
- SFT datasets: 10K-100K examples, quality over quantity
- Preference data: human-annotated comparisons (chosen vs rejected)
- Post-training typically takes hours to days, not weeks to months
- Model personality, style, and refusal behavior are primarily shaped here
- Constitutional AI: model self-critiques guided by written principles
- Red-teaming: adversarial testing to find failure modes before deployment
- The same techniques are available for enterprise customization

## Related Terms

- [Supervised Fine-Tuning](supervised-fine-tuning.md)
- [RLHF & Alignment Techniques](rlhf-and-alignment-techniques.md)
- [Alignment](alignment.md)
- [Pre-training](pre-training.md)
- [Transfer Learning](transfer-learning.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
