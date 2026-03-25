# LLM as a Judge / Agent as a Judge

LLM as a Judge is the practice of using powerful language models to evaluate the outputs of other models, replacing or augmenting human evaluation at scale. It achieves 80-85% agreement with human annotators and has become essential infrastructure for model development, quality monitoring, and comparative assessment.

## How It Works

The core idea is straightforward: present a capable model (the judge) with outputs from another model (the subject) and ask it to evaluate quality along defined dimensions. The judge model receives the original prompt, the subject's response, and evaluation criteria, then produces a score, ranking, or qualitative assessment.

LLM-as-a-Judge is used in three primary contexts. During model development, it provides rapid feedback on training experiments without waiting for human annotators. In production quality monitoring, it continuously evaluates model outputs against quality standards, flagging degradation. For model comparison, it provides pairwise judgments (which response is better?) that scale beyond what human evaluation can support.

When evaluating AI agents rather than simple model responses, the approach extends to "Agent as a Judge." Here the evaluator assesses not just the final output but the entire trajectory: did the agent use the right tools, in the right order, with the right parameters? Did it recover gracefully from errors? Trajectory evaluation is more complex than output evaluation because it requires understanding multi-step reasoning and tool use.

The technique has known limitations. Judge models exhibit biases: preference for longer responses, sensitivity to output order (preferring whichever response is presented first), and tendency to favor responses that match their own style. Blind spots exist where the judge model lacks knowledge to evaluate correctness. Mitigation strategies include randomizing presentation order, using multiple judges, and combining LLM judgment with deterministic checks.

**Process Reward Models (PRMs)** vs **Outcome Reward Models (ORMs)** represent a critical distinction in how evaluation signals are generated. ORMs evaluate only the final answer: correct or incorrect. PRMs provide feedback at each reasoning step, identifying exactly where reasoning goes wrong. Research from OpenAI demonstrated that PRMs achieve 78.2% accuracy on the MATH benchmark compared to 72.4% for ORMs. Step-by-step verification enables advanced search strategies like Monte Carlo Tree Search (MCTS) and Best-of-N sampling, where the model generates multiple solution paths and PRMs select the best trajectory through the reasoning space.

## Medical Analogy

LLM as a Judge is peer review. When a physician submits research for publication, other physicians evaluate the quality, methodology, and conclusions. Peer reviewers are not infallible; they bring their own biases and blind spots. But the process, at scale, is the best mechanism available for quality assurance. PRMs are like an attending physician reviewing a resident's diagnostic process step by step, catching reasoning errors before they affect the final diagnosis, rather than only checking whether the final diagnosis is correct.

## Why It Matters for Enterprise AI

Evaluation at scale is the bottleneck that prevents most enterprises from iterating on AI quality. The $252B invested in AI produced models that need continuous evaluation, but human evaluation does not scale. The 42% of abandoned initiatives often cite an inability to measure whether the AI is actually performing well. LLM-as-a-Judge gives you a scalable evaluation layer. But the judge is only as good as its criteria. Generic evaluation criteria produce generic assessments. When you define evaluation rubrics grounded in your institutional standards, your compliance requirements, your quality benchmarks, you turn a commodity evaluation tool into a force multiplier for quality assurance. Your ground truth about what constitutes excellence in your domain is the codified craftsmanship that makes automated evaluation meaningful. Without domain-specific criteria, you are grading by someone else's standards.

## Key Technical Details

- Agreement with humans: 80-85% on well-defined evaluation tasks
- Common judges: GPT-4, Claude 3.5 Sonnet, specialized reward models
- Biases: verbosity preference, position bias, self-preference, style matching
- Mitigations: randomize order, use multiple judges, combine with deterministic checks
- PRMs: per-step feedback; 78.2% on MATH benchmark (vs 72.4% for ORMs)
- ORMs: final-answer-only feedback; simpler but less informative
- MCTS + PRMs: search over reasoning paths using step-level scores
- Best-of-N sampling: generate N responses, use judge to select best
- Agent evaluation: assess tool use, trajectory quality, error recovery
- Cost-effective: 10-100x cheaper than human evaluation at comparable quality

## Related Terms

- [Benchmarks](benchmarks.md)
- [Evaluation Data](evaluation-data.md)
- [Alignment](alignment.md)
- [Reinforcement Learning](reinforcement-learning.md)
- [RLHF & Alignment Techniques](rlhf-and-alignment-techniques.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
