# Chain of Thought (CoT)

Chain of Thought is the technique of having an LLM show its reasoning steps before arriving at a final answer. Eliciting intermediate reasoning steps improves accuracy by 20-40% on complex tasks compared to direct answer generation.

## How It Works

When you ask an LLM a complex question directly, it generates the answer token by token from the prompt alone. The model must compress all reasoning into the implicit computation of its forward pass. Chain of Thought changes this by giving the model space to think on paper: break the problem into steps, work through each one, and arrive at the answer through explicit intermediate reasoning.

There are three main variants. Few-shot CoT provides examples of step-by-step reasoning in the prompt, teaching the model the expected format through demonstration. Zero-shot CoT is simpler and remarkably effective: appending "Let's think step by step" to a prompt triggers reasoning behavior without any examples. The model has seen enough reasoning traces in its training data that this simple instruction activates the pattern.

Trained CoT represents the third and most powerful approach. Models like OpenAI's o1 and DeepSeek-R1 are explicitly trained through reinforcement learning to generate internal chains of thought before producing answers. These models think before they speak as a fundamental capability, not a prompting trick. The reasoning traces may be visible (as with DeepSeek-R1's open approach) or hidden behind an API (as with o1's "thinking" tokens that users cannot see).

The mechanism works because language models are autoregressive: each generated token becomes context for the next. When a model writes "First, let's identify the key variables..." that text becomes part of what it conditions on for subsequent generation. The reasoning steps are not merely cosmetic; they literally change the probability distribution over future tokens by providing richer context.

The accuracy gains are most pronounced on tasks requiring arithmetic, multi-step logic, commonsense reasoning, and domain-specific analysis. On the GSM8K math benchmark, chain-of-thought prompting improved accuracy from roughly 18% to 57% for PaLM 540B. The gains scale with model size: smaller models sometimes produce plausible-looking but incorrect reasoning chains, while larger models more reliably generate valid ones.

## Medical Analogy

Chain of thought is the medical equivalent of "show your work." A physician who announces a diagnosis without explanation is less trustworthy and more error-prone than one who walks through their differential: "The patient presents with X, which suggests A or B. Given the lab results showing Y, A is more likely. However, we should rule out C because of the family history." That explicit reasoning process catches errors that gut instinct misses and lets colleagues verify the logic.

## Why It Matters for Enterprise AI

Chain of thought is your audit trail. In enterprise contexts where decisions have consequences, you need to understand why an AI system reached a particular conclusion, not just what it concluded. The 42% of AI initiatives that get abandoned often fail the trust test: stakeholders cannot verify the system's reasoning, so they do not trust its outputs.

When you combine chain of thought with your institutional knowledge through RAG, you get something powerful: an AI system that reasons using your ground truth and shows you exactly how it got from your data to its conclusion. That transparency transforms AI from a black box into a collaborative tool. Your domain experts can review the reasoning chain, catch errors the model makes, and refine the process. This is codified craftsmanship in action: the model's reasoning follows the analytical frameworks your best people have developed.

## Key Technical Details

- Few-shot CoT: include reasoning examples in the prompt (2-5 examples typical)
- Zero-shot CoT: append "Let's think step by step" or similar instruction
- Trained CoT: models like o1 and DeepSeek-R1 with RL-trained internal reasoning
- Accuracy improvement: 20-40% on complex multi-step tasks
- GSM8K benchmark: PaLM 540B went from ~18% to ~57% with CoT prompting
- Gains scale with model size; smaller models may generate plausible but incorrect chains
- Internal vs visible traces: o1 hides reasoning tokens; DeepSeek-R1 exposes them
- CoT tokens consume compute budget and increase latency

## Related Terms

- [Reasoning](reasoning.md) - the cognitive capability CoT makes visible
- [Inference](inference.md) - the runtime process where CoT generation occurs
- [Prompt Engineering](prompt-engineering.md) - the discipline that includes CoT techniques
- [Hallucination](hallucination.md) - CoT can expose or sometimes amplify confabulation

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
