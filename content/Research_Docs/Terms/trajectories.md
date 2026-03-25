# Trajectories

Trajectories are the complete sequence of thoughts, decisions, tool calls, observations, and actions that an agent takes to accomplish a goal. They are the recorded pathway from objective to outcome, capturing not just what was done but how and why.

## How It Works

When an agent works on a task, it generates a trajectory: an ordered sequence of steps, each consisting of a Thought (the model's reasoning about what to do next), an Action (a tool call or output generation), and an Observation (the result of that action). This Thought → Action → Observation loop repeats until the agent determines the goal is achieved or it cannot proceed further.

A trajectory is not a rigid script. It is an adaptive plan that evolves based on intermediate results. If a database query returns unexpected results, the agent adjusts its next step. If a tool call fails, the agent reasons about alternatives. If new information contradicts earlier assumptions, the agent revises its approach. This adaptability is what distinguishes agent trajectories from deterministic automation scripts that follow the same path regardless of conditions.

Trajectory quality depends on two factors: the model's reasoning capability and the quality of available context. A strong reasoning model working with poor tools and sparse knowledge produces trajectories that reason well but execute poorly. A weak reasoning model with excellent tools and rich context produces trajectories that have the right resources but make poor decisions about how to use them. The best trajectories emerge from strong reasoning grounded in rich, domain-specific context through RAG.

Trajectory evaluation is how agent performance is measured. Since agent tasks are complex and open-ended, simple accuracy metrics do not capture quality. LLM-as-Judge evaluation uses a second model to assess trajectory quality against defined rubrics: Did the agent pursue an efficient path? Did it use appropriate tools? Did it handle errors correctly? Did it arrive at the right conclusion? Expert-written rubrics define what "good" looks like for each task type, establishing quality standards that evaluation models apply.

Trajectory logging provides the audit trail for enterprise agent deployments. Every thought, tool call, observation, and decision is recorded, creating a complete record of what the agent did and why. This serves compliance requirements, enables debugging, and provides training data for improving future agent performance.

## Medical Analogy

A trajectory is a care pathway: the documented sequence of clinical decisions from patient presentation to treatment outcome. A physician sees a patient (goal), takes a history (thought + observation), orders labs (action), interprets results (observation), forms a differential (thought), prescribes treatment (action), monitors response (observation), and adjusts as needed (adaptive planning). The complete pathway is documented in the medical record, serving as both the audit trail and the learning resource. Standardized care pathways, developed by clinical experts, provide the template that individual trajectories follow while allowing adaptation to specific patient circumstances.

## Why It Matters for Enterprise AI

Trajectories are where your institutional knowledge becomes most directly valuable. Your documented processes, your workflow runbooks, your decision trees, and your escalation procedures are trajectory templates. They define the expected path through complex organizational tasks, including the branching logic for different scenarios and the quality criteria for each step.

The 42% of abandoned AI initiatives and >80% with no meaningful EBIT impact often lacked defined trajectories. They deployed agents without specifying what "good" looks like for their specific tasks. Without expert-written rubrics defining quality standards, there is no way to evaluate whether an agent is performing well or badly. Without documented processes providing trajectory templates, agents improvise in ways that may violate organizational norms.

Your domain experts are the trajectory architects. They know the efficient path through your processes, the edge cases that require special handling, the quality checkpoints that catch errors before they propagate. When you codify that expertise into trajectory templates and evaluation rubrics, you create the infrastructure for agents that work the way your best people work. That codified craftsmanship is the strategic moat: competitors can deploy the same model and the same tools, but they cannot replicate the trajectory patterns that encode your organizational intelligence.

## Key Technical Details

- Core loop: Thought → Action → Observation → Repeat
- Adaptive planning: trajectories adjust based on intermediate results, not rigid scripts
- Quality factors: reasoning capability + context quality determine trajectory quality
- LLM-as-Judge evaluation: second model assesses trajectories against defined rubrics
- Expert-written rubrics: define quality standards for specific task types
- Trajectory logging: complete audit trail of every thought, action, and observation
- Training data: logged trajectories improve future agent performance
- Trajectory templates: documented processes that define expected agent behavior patterns

## Related Terms

- [Agents](agents.md) - the systems that generate trajectories
- [Reasoning](reasoning.md) - the cognitive capability driving trajectory decisions
- [Tool Use](tool-use.md) - the actions within trajectories
- [Agent Harnesses](agent-harnesses.md) - the infrastructure that captures and manages trajectories

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
