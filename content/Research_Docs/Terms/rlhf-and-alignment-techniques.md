# RLHF & Alignment Techniques

RLHF (Reinforcement Learning from Human Feedback) and its successors are the techniques used to align language model behavior with human preferences. This family of methods spans from the original reward-model-based RLHF/PPO to direct preference optimization (DPO), integrated approaches (ORPO), and group-based methods (GRPO) that scale reasoning capabilities.

## How It Works

**RLHF with PPO** is the original alignment technique, used for GPT-4 and early Claude models. The process has three stages: (1) collect human comparisons where annotators rank model outputs from best to worst, (2) train a reward model that predicts human preferences from these comparisons, and (3) optimize the language model using Proximal Policy Optimization (PPO) to maximize the reward model's scores. PPO uses a clipped surrogate loss function that prevents catastrophically large policy updates. A KL divergence penalty keeps the model from drifting too far from its SFT baseline. RLHF/PPO is powerful but complex: it requires training and maintaining a separate reward model, managing training stability, and balancing multiple loss terms.

**DPO (Direct Preference Optimization)** eliminates the separate reward model entirely. Instead, DPO directly optimizes the language model on preference pairs (chosen vs rejected responses) using an implicit reward derived from the log-likelihood ratio between the policy model and a reference model. The math is elegant: it proves that the optimal policy under the RLHF objective can be expressed in closed form. DPO is significantly simpler to implement and more stable to train. However, research suggests PPO may still produce stronger results for complex reasoning tasks where exploration is valuable.

**ORPO (Odds Ratio Preference Optimization)** integrates alignment into the SFT stage, eliminating the need for a separate alignment phase entirely. It combines the standard SFT loss with an odds ratio penalty that discourages generating rejected responses. This one-stage approach reduces training time and compute requirements.

**GRPO (Group Relative Policy Optimization)**, developed by DeepSeek, eliminates the need for both a reward model and a critic model. For each prompt, GRPO generates a group of outputs, scores them (often via verifiable rewards for math/code), and computes advantages relative to the group mean. This group-based advantage estimation is computationally efficient and was central to DeepSeek-R1's reasoning capabilities.

| Method | Reward Model | Stages | Strength | Limitation |
|--------|-------------|--------|----------|------------|
| RLHF/PPO | Required | 3 | Complex reasoning, exploration | Unstable, expensive |
| DPO | Eliminated | 2 | Stable, simple implementation | Limited exploration |
| ORPO | Eliminated | 1 | Efficient, integrated | Less flexible |
| GRPO | Eliminated | 2 | Efficient reasoning scaling | Needs verifiable rewards |

## Medical Analogy

These are different models for supervising a medical resident. RLHF/PPO is like having a dedicated attending who scores every decision, and the resident optimizes to satisfy that attending. DPO is like giving the resident paired cases (this treatment worked, that one did not) and letting them internalize the preference directly. ORPO is like integrating evaluation into every teaching moment during rounds. GRPO is like reviewing a batch of the resident's cases together, comparing outcomes within the group to identify what worked best.

## Why It Matters for Enterprise AI

Alignment techniques determine whether AI behaves according to your organization's values and standards. The $252B AI investment produced powerful models, but the over 80% showing no meaningful EBIT impact often suffer from misalignment: the model is capable but does not behave the way your organization needs. DPO and GRPO have made alignment accessible to enterprises. You do not need Google-scale infrastructure to align a model to your preferences. Collect examples of preferred and rejected outputs from your domain experts, and DPO can encode those preferences directly. Your ground truth about what constitutes a good response in your context, that is tribal knowledge that no foundation model provider can replicate. Alignment is where codified craftsmanship meets scalable deployment.

## Key Technical Details

- RLHF/PPO: reward model + clipped surrogate loss + KL penalty; 3-stage pipeline
- DPO: log-likelihood ratio optimization; closed-form optimal policy; 2-stage
- ORPO: SFT + odds ratio penalty; single-stage alignment
- GRPO: group-based advantage; no critic model; used in DeepSeek-R1
- Preference data: pairs of chosen/rejected responses ranked by humans
- KL divergence: constrains aligned model to stay near the SFT checkpoint
- PPO clips gradient updates to prevent instability (epsilon typically 0.2)
- DPO beta parameter controls deviation from reference model (typically 0.1-0.5)

## Related Terms

- [Reinforcement Learning](reinforcement-learning.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)
- [Alignment](alignment.md)
- [Post-training](post-training.md)
- [LLM as a Judge](llm-as-a-judge.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
