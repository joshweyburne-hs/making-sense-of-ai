# Reasoning

Reasoning is the capacity of an LLM to go beyond simple retrieval and pattern matching to perform multi-step, analytical problem solving. It represents the shift from "what word comes next" to "let me think through this systematically before answering."

## How It Works

The distinction between basic LLM inference and reasoning maps cleanly to Daniel Kahneman's System 1 / System 2 framework. Standard token prediction is System 1 thinking: fast, automatic, associative. The model sees a prompt and immediately begins generating the most probable next token. This works remarkably well for straightforward tasks but falls apart when problems require planning, decomposition, or logical deduction.

Reasoning models introduce System 2 thinking: slow, deliberate, analytical processing. Large Reasoning Models (LRMs) like OpenAI's o1 series and DeepSeek-R1 are trained to pause and think before answering. They generate an internal chain of thought, breaking complex problems into sub-steps, evaluating intermediate conclusions, and sometimes backtracking when a line of reasoning fails.

The training mechanism is reinforcement learning rather than supervised fine-tuning. Instead of showing the model examples of correct reasoning traces, RL rewards the model for arriving at correct final answers, letting it discover effective reasoning strategies on its own. DeepSeek-R1 demonstrated this dramatically: pure RL training produced emergent chain-of-thought behavior without any supervised reasoning examples.

The practical breakthrough is test-time compute scaling. Traditional scaling laws focused on making models bigger (more parameters) or training them longer (more data). Reasoning models scale at inference time instead, dynamically allocating more computation to harder problems. A 7-billion parameter model given extended deliberation time can match or exceed a 70-billion parameter model that answers immediately. This inverts the economics: instead of paying for massive models on every query, you pay for extended thinking only when problems demand it.

The implications compound when reasoning combines with tool use. A reasoning model does not just think harder; it plans which tools to call, in what order, evaluates intermediate results, and adjusts its approach. This is the foundation of agentic behavior.

## Medical Analogy

Reasoning is the difference between a medical student reciting textbook definitions and a physician working through a differential diagnosis. The student retrieves; the physician reasons. When a patient presents with chest pain, the physician does not jump to the first association. They systematically consider cardiac, pulmonary, gastrointestinal, and musculoskeletal causes, weigh evidence from the history, order targeted tests, and narrow the differential. That deliberate process is reasoning.

## Why It Matters for Enterprise AI

Reasoning is what separates AI that handles FAQs from AI that handles your actual business problems. Most enterprise challenges are not single-hop retrieval questions. They require synthesizing information across multiple sources, applying domain-specific logic, and making judgment calls under uncertainty. The $252B invested in AI has overwhelmingly funded systems that retrieve and summarize. The >80% that show no meaningful EBIT impact often failed precisely because retrieval alone was not enough.

Your institutional knowledge becomes the force multiplier here. A reasoning model working with your documented decision frameworks, your escalation criteria, your risk assessment rubrics can replicate the multi-step thinking your best people do. Without that codified craftsmanship, the model reasons in a vacuum. With it, you have a system that thinks the way your organization thinks, at scale.

## Key Technical Details

- System 1 (standard LLMs): ~instant token prediction, no deliberation, good for routine tasks
- System 2 (reasoning models): extended inference, internal chain of thought, suited for complex analysis
- Test-time compute scaling: allocate more computation dynamically at inference for harder problems
- Training via RL: models discover reasoning strategies through reward signals, not supervised examples
- DeepSeek-R1: demonstrated emergent reasoning from pure RL without supervised chain-of-thought data
- A 7B parameter model with extended reasoning can match a 70B model answering immediately
- Reasoning tokens are typically hidden from the user but consume compute budget

## Related Terms

- [Chain of Thought](chain-of-thought.md) - the visible manifestation of reasoning
- [Inference](inference.md) - the runtime where reasoning occurs
- [Agents](agents.md) - reasoning combined with tool use and action
- [Trajectories](trajectories.md) - the recorded path of reasoning and action

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
