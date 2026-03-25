# Reinforcement Learning

Reinforcement learning (RL) is a training paradigm where a model learns by generating outputs, receiving reward signals, and adjusting its behavior to maximize those rewards over time. Unlike supervised fine-tuning which teaches by example, RL teaches by outcome, enabling models to discover strategies that no human demonstrated.

## How It Works

The core RL loop is straightforward: the model generates an output, a reward function scores that output, and the model's parameters are adjusted to increase the probability of high-scoring outputs and decrease the probability of low-scoring ones. This generate-score-adjust cycle repeats millions of times.

RL has a rich history beyond language models. DeepMind's AlphaGo used RL to discover Go strategies no human had conceived. Robotics uses RL to learn physical manipulation through trial and error. Game-playing agents use RL to achieve superhuman performance in Atari, StarCraft, and DOTA. The unifying principle is that explicit demonstrations are insufficient or unavailable, so the agent must explore and learn from consequences.

In the LLM context, RL refines behavior after supervised fine-tuning. SFT teaches the model what good responses look like. RL teaches the model to actively seek better responses by optimizing for a reward signal. The model generates multiple candidate responses, each is scored, and the model updates its policy to favor higher-scoring outputs.

The reward signal can come from several sources. In RLHF (Reinforcement Learning from Human Feedback), a separate reward model trained on human preference data provides scores. In RLVR (Reinforcement Learning from Verifiable Rewards), the reward comes from objective verification: does the code pass the test suite? Is the math answer correct? RLVR has proven especially effective for mathematics and code, where correctness is binary and easily verified. DeepSeek-R1 used RLVR extensively to improve mathematical reasoning.

The key technical challenge in RL for LLMs is credit assignment: determining which parts of a long response contributed to its quality. Policy gradient methods like PPO (Proximal Policy Optimization) handle this by estimating advantage functions that measure how much better or worse each action was compared to baseline. The clipped surrogate objective prevents catastrophically large updates that could destabilize training.

## Medical Analogy

Reinforcement learning is independent clinical practice with outcome tracking. After residency, a physician treats patients and observes outcomes. A treatment that leads to recovery is reinforced. A treatment that leads to complications is adjusted. Over years of practice, the physician develops judgment that transcends what any textbook or attending physician explicitly taught. They discover approaches through experience that nobody demonstrated for them. RL gives models the same opportunity to discover improved strategies through feedback rather than imitation.

## Why It Matters for Enterprise AI

RL represents the frontier of enterprise AI customization. While SFT lets you teach a model your patterns, RL lets you optimize a model against your actual success metrics. The $252B invested in AI has largely produced models trained on generic reward signals. The over 80% that show no meaningful EBIT impact are optimizing for the wrong outcomes. When you define reward functions grounded in your business metrics, customer satisfaction scores, compliance pass rates, or deal close rates, RL becomes the mechanism that continuously improves your AI against the metrics that actually matter to your organization. Your ground truth becomes the reward signal. That is codified craftsmanship operating as a force multiplier, tuning a model not just to imitate your best practices but to optimize for your actual outcomes.

## Key Technical Details

- Core loop: generate → score → adjust parameters → repeat
- Policy gradient methods: PPO (clipped surrogate objective), REINFORCE
- RLHF: reward model trained on human preferences provides scores
- RLVR: verifiable rewards for math (correct answer) and code (passes tests)
- Credit assignment: determining which actions contributed to the reward
- Exploration vs exploitation: balancing trying new strategies vs using known good ones
- KL divergence penalty: prevents the model from drifting too far from the SFT baseline
- RL training is less stable than SFT and requires careful hyperparameter tuning
- DeepSeek-R1 demonstrated that RL alone (without SFT) can produce strong reasoning

## Related Terms

- [Supervised Fine-Tuning](supervised-fine-tuning.md)
- [RLHF & Alignment Techniques](rlhf-and-alignment-techniques.md)
- [Alignment](alignment.md)
- [Post-training](post-training.md)
- [Benchmarks](benchmarks.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
