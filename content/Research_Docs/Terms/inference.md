# Inference

Inference is the real-time moment when an LLM applies everything it learned during training to generate a response. It is the point where billions of dollars in training investment meets your specific question, right now, token by token.

## How It Works

Every phase of the LLM pipeline, pre-training on trillions of tokens, supervised fine-tuning, reinforcement learning from human feedback, converges at inference. The model receives your prompt, processes it through its layers of attention and feed-forward networks, and produces a probability distribution over its entire vocabulary for the next token. It samples from that distribution, appends the chosen token to its context, and repeats. This autoregressive loop continues until the model generates a stop token or hits a length limit.

The process is fundamentally probabilistic, not deterministic. The same prompt can produce different outputs across runs because token selection involves sampling from probability distributions. Temperature controls the randomness: low temperature (0.1-0.3) makes the model conservative, heavily favoring the most probable tokens. High temperature (0.8-1.0) flattens the distribution, allowing more diverse and creative outputs. Top-p (nucleus) sampling provides another control by considering only the smallest set of tokens whose cumulative probability exceeds a threshold.

Test-time compute scaling has transformed inference from a fixed-cost operation into a variable one. Traditional inference ran a single forward pass per token. Reasoning models allocate additional computation for complex problems, generating internal chains of thought that consume extra tokens and time. This means a single query might use 10x the compute of a simple one, but produce dramatically better results on hard problems.

Cost considerations dominate enterprise inference decisions. You pay per token generated, and costs vary by orders of magnitude across model sizes. A GPT-4 class model might cost 100x more per token than a smaller model. Techniques like quantization (reducing parameter precision from 32-bit to 8-bit or 4-bit), distillation (training smaller models to mimic larger ones), and speculative decoding (using a small model to draft tokens verified by a large model) all aim to reduce inference cost without proportional quality loss.

Latency matters as much as cost. Users expect responses in seconds, not minutes. Batching multiple requests, KV-cache optimization (reusing computed attention states for unchanged context), and hardware choices (GPUs vs specialized inference chips) all factor into making inference fast enough for production use.

## Medical Analogy

Inference is the clinical encounter. Everything the physician learned in medical school, residency, and years of practice comes to bear in the moment they examine a patient and make a decision. The training shaped the physician's judgment, but inference is where that judgment meets reality. And like medicine, the outcome is probabilistic: the same symptoms might lead a physician toward different hypotheses on different days depending on subtle contextual cues.

## Why It Matters for Enterprise AI

Inference is where you either get value from AI or you do not. Every dollar of the $252B invested in AI ultimately needs to produce useful inference. The >80% of organizations seeing no meaningful EBIT impact from AI often have a mismatch between inference cost and business value: they are running expensive models on low-value tasks, or cheap models on high-stakes decisions.

Your strategic moat at inference time is context quality. Two organizations running identical models will get different results based on what they feed the model at inference. Your curated institutional knowledge, your documented processes, your domain-specific ground truth, all injected via RAG at inference time, is what transforms generic capability into organizational value. The model is the same for everyone. What you give it to work with is not.

## Key Technical Details

- Autoregressive generation: one token at a time, each conditioned on all previous tokens
- Temperature: controls randomness (0.0 = greedy/deterministic, 1.0 = maximum diversity)
- Top-p sampling: considers only tokens within cumulative probability threshold p
- KV-cache: stores computed attention key-value pairs to avoid redundant computation
- Quantization: INT8 or INT4 reduces memory and cost with modest quality trade-offs
- Speculative decoding: small model drafts, large model verifies, speeds generation 2-3x
- Token costs: vary 10-100x across model sizes; enterprise cost optimization is critical
- Latency targets: <2 seconds for interactive use, <500ms for real-time applications

## Related Terms

- [Reasoning](reasoning.md) - extended inference with test-time compute scaling
- [Chain of Thought](chain-of-thought.md) - visible reasoning during inference
- [Context Windows](context-windows.md) - the capacity constraint during inference
- [Hallucination](hallucination.md) - the primary failure mode during inference

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
