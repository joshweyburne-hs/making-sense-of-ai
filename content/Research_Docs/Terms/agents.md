# Agents

Agents are LLM systems that go beyond answering questions to taking autonomous action: planning multi-step workflows, using tools, observing results, and adapting their approach based on what they find. They represent the frontier of AI value creation.

## How It Works

A standard LLM interaction is reactive: you ask a question, it generates an answer. An agent is proactive. Given a goal, it decomposes the objective into sub-tasks, determines which tools and information it needs, executes actions, evaluates the results, and adjusts its plan accordingly. The loop is: Think (reason about the next step) -> Act (execute a tool call or generate output) -> Observe (process the result) -> Repeat until the goal is achieved.

The evolution from chatbot to agent happened in three phases, as mapped by enterprise deployment patterns. Phase one was single-turn chat: ask a question, get an answer. Useful for FAQ-style interactions but fundamentally limited. Phase two introduced reasoning and tool use: the model could think through complex problems and call external tools to retrieve data or perform calculations. This was the breakthrough that enabled AI to do work rather than just discuss it. Phase three is agentic workflows: multi-step, multi-tool processes that run with varying degrees of autonomy, from human-in-the-loop approval at each step to fully autonomous execution within defined boundaries.

Enterprise agent maturity follows a V0-V4 progression. V0 is a chatbot with no tool access. V1 adds basic tool use (database queries, API calls). V2 introduces multi-step workflows with error handling and retry logic. V3 enables collaboration between multiple specialized agents, each with domain-specific tools and knowledge. V4 is a fully autonomous agent operating within defined governance boundaries, able to handle novel situations by composing capabilities it has not been explicitly programmed for.

The gap between a chatbot and an agent is the gap between knowing about medicine and practicing medicine. A chatbot can tell you the symptoms of pneumonia. An agent can review the patient chart, order the appropriate labs, check for drug interactions with current medications, schedule the follow-up, and document everything in the medical record.

## Medical Analogy

An agent is a practicing physician, not a medical encyclopedia. The encyclopedia contains knowledge; the physician applies it. Given a patient presenting with symptoms, the physician does not just list possible diagnoses. They take a history, order tests, interpret results, form a differential, choose a treatment plan, monitor the response, and adjust. Each step informs the next. The physician uses tools (stethoscope, lab tests, imaging), consults references (guidelines, specialists), and adapts to unexpected findings. That entire loop of reasoning, action, and adaptation is what makes an agent.

## Why It Matters for Enterprise AI

Agents are where the $252B invested in AI starts generating compound returns. Chatbots automate information retrieval; agents automate workflows. The difference in business value is orders of magnitude. A chatbot that answers questions about your expense policy saves minutes. An agent that processes expense reports, flags anomalies, routes approvals, and updates accounting systems saves headcount-equivalent hours across thousands of transactions.

The 42% abandonment rate and <25% pilot-to-production conversion are largely pre-agent statistics. Organizations tried to extract workflow-level value from question-answering tools. Agents close that gap, but only when grounded in your institutional knowledge. An agent that does not understand your approval hierarchy, your escalation procedures, your compliance requirements is not just useless; it is dangerous. Your documented processes become the agent's playbook. Your decision frameworks become its reasoning scaffold. Your domain expertise, codified into tools, knowledge bases, and quality rubrics, is the force multiplier that transforms a generic agent into one that works the way your organization works.

## Key Technical Details

- Core loop: Think → Act → Observe → Repeat
- Three-phase evolution: single-turn chat → reasoning + tool use → agentic workflows
- V0-V4 maturity: chatbot → basic tools → multi-step → multi-agent → autonomous
- Tool use: agents call external systems (APIs, databases, search, compute)
- Planning: agents decompose complex goals into sub-tasks before execution
- Error handling: agents detect failures, retry with different approaches, escalate when stuck
- Human-in-the-loop: configurable autonomy from full approval to bounded autonomy
- Multi-agent: specialized agents collaborate on complex workflows

## Related Terms

- [Agent Harnesses](agent-harnesses.md) - the infrastructure that enables agents
- [Tool Use](tool-use.md) - how agents interact with external systems
- [Trajectories](trajectories.md) - the recorded path of agent reasoning and action
- [Reasoning](reasoning.md) - the cognitive capability that powers agent planning
- [RAG](rag.md) - the knowledge retrieval mechanism agents depend on

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
