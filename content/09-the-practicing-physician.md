# The Practicing Physician: Agents in Action

*Part 9 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Agents, Agent Harnesses, Tool Use, Trajectories
*For deeper technical dives on each term, see the [Term Reference Library](Research_Docs/Terms/).*

---

## The Problem

Deploying a model on a single task is table stakes. Building a system you trust to automate full workflows — multi-step, judgment-intensive, exception-heavy — is the hard part. And it's where the real enterprise value lives. Of the $252 billion in corporate AI investment, >80% of organizations report no meaningful EBIT impact, largely because they never graduate from single-task automation (V0) to the agentic workflows (V1-V4) that actually transform operations. The gap isn't intelligence. It's the human knowledge and evaluation infrastructure that makes AI trustworthy enough to act autonomously.

---

## The Medical Scenario

Dr. Patel has completed all her training. She's not answering questions anymore — she's *practicing medicine.* On a typical day, she reviews charts, orders tests, interprets results, adjusts treatment plans, consults specialists, prescribes medications, documents in the EMR, and follows up as new data arrives.

She isn't waiting for someone to ask her a question. She's autonomously managing a workflow — taking actions, using tools, making decisions, and adapting as circumstances change. The hospital infrastructure around her — EMR, lab system, pharmacy, scheduling, referral network — enables her to practice effectively.

This is the final stage of the medical training journey, and it's where LLMs are heading: from assistants that answer questions to **agents** that take action.

---

## The V0-V4 Maturity Model: From Task to Team

Not all agent deployments are equal. Think of it as levels of medical practice:

**V0 — Single Tasks (Medical Student):** Summarize this chart. Answer this question. One task, one response, done. This is where most organizations are today. It's useful, but it's a fraction of the value.

**V1 — Single Long-Horizon (Resident, supervised):** Complete a multi-step research task. Prepare a meeting brief by pulling data from five systems, synthesizing it, and drafting talking points. One goal, many steps, sustained effort.

**V2 — Interactive Complex (Attending, consulting):** Handle a complex workflow that requires back-and-forth with users, judgment calls at decision points, and adaptation when circumstances change. Think: managing a deal-desk approval process end-to-end.

**V3 — Full Role (Specialist, autonomous):** Operate an entire function — customer onboarding, benefits administration, compliance review — with human oversight on exceptions only.

**V4 — Full Team Orchestration (Department Chief):** Coordinate multiple agents working together, each handling a role, with one agent managing prioritization, resource allocation, and escalation across the team.

Each level requires exponentially more human data infrastructure. V0 needs a prompt. V4 needs mapped workflows, captured expert decisions, evaluation rubrics, and feedback loops. This is why the three enterprise barriers from [Post 8](08-the-medical-library.md) — no workflow understanding, no decision capture, no feedback loops — become more critical at every level.

Every enterprise function has the same pattern of inconsistency that agents can solve: benefits administration, compliance review, underwriting, immigration processing, claims adjudication. Your best people handle these differently from your average people. The gap between best and average is tribal knowledge. Agents encode the best and scale it.

---

## Agents: The Doctor in Practice

For most of this series, you've been looking at LLMs as they've traditionally been used: ask a question, get an answer. That's asking a doctor a medical question at a dinner party — useful, but a fraction of what a trained physician can do.

An **agent** is an LLM that can take actions, not just generate text:

- **Make decisions** about what to do next based on a goal
- **Use tools** to interact with external systems
- **Observe results** and decide on the next step
- **Iterate** through multiple steps for a complex task
- **Adapt** when things don't go as expected

The difference between a chatbot and an agent is the difference between a doctor answering medical trivia and a doctor managing a patient's care. The chatbot knows things. The agent *does* things.

A sales rep asks a traditional assistant: "How should I approach the Acme renewal?" The LLM gives general advice.

Now imagine an agent. The rep says: "Prepare for my Acme renewal meeting tomorrow." The agent:

1. Pulls Acme's account history from the CRM
2. Reviews the last three support tickets for pain points
3. Checks product usage analytics for feature adoption
4. Looks up the competitive landscape for Acme's industry
5. Reviews contract terms and identifies upsell opportunities
6. Drafts a personalized meeting agenda with talking points
7. Sends the prep document to the rep's email

That's not a chatbot. That's a digital colleague that takes a goal and works through it.

> **Simplification Note:** "Agent" is used broadly and the industry hasn't settled on a single definition. Some define agents as fully autonomous systems. Others define them more practically as LLMs with tool use and multi-step planning. For this series, an agent is an AI system that can plan, use tools, and take multi-step actions toward a goal — with varying degrees of human oversight depending on the use case and risk level.

*Deep dive: [Agents](Research_Docs/Terms/agents.md)*

---

## Agent Harnesses: The Hospital System

No doctor practices in isolation. Dr. Patel is effective because she operates within a hospital system that connects her to everything she needs. Without that infrastructure, even the best doctor is scribbling notes on paper and calling labs on the phone.

An **agent harness** (also called an agent framework or orchestration layer) is the infrastructure that enables an AI agent to operate:

**Tool registration:** A catalog of tools the agent can use — APIs, databases, systems. Like a hospital's directory of services and departments.

**Orchestration:** The logic managing the agent's workflow — when to use a tool, how to handle responses, how to pass information between steps. Like hospital workflow management coordinating between departments.

**Memory and state management:** Tracking what the agent has done, what it's gathered, and where it is in a multi-step process. Like the patient chart tracking the full history of care.

**Safety and permissions:** Controlling what the agent can do. Read data? Write data? Send emails? Execute transactions? Like hospital privileges determining what procedures a doctor is authorized to perform.

**Error handling:** Managing tool failures, unexpected results, and stuck states. Like escalation procedures when a case exceeds a resident's expertise.

Popular harnesses include LangChain, LlamaIndex, Microsoft AutoGen, CrewAI, and Snowflake's Cortex Agents. The specific framework matters less than the concept: agents need infrastructure to act, and the harness determines the ceiling of what they can do.

> **Simplification Note:** The agent harness landscape evolves rapidly. New frameworks emerge monthly. Choosing a harness is an architectural decision similar to choosing a hospital information system — it determines what your agents can do and how they interact with your existing systems.

*Deep dive: [Agent Harnesses](Research_Docs/Terms/agent-harnesses.md)*

---

## Tool Use: The Doctor's Instruments

A doctor's knowledge alone isn't sufficient. Diagnosing requires instruments: stethoscopes, imaging, lab tests. Treating requires tools: surgical instruments, prescription systems, monitoring devices. Every tool extends capability beyond what's possible with knowledge alone.

**Tool use** is how agents interact with the world beyond text generation:

**Data retrieval tools:** Query a CRM, pull records, search a knowledge base. Like accessing patient records.

**Computation tools:** Run calculations, execute code, process data. Like a clinical calculator for medication dosages.

**Communication tools:** Send emails, post messages, create tickets. Like placing a consultation request.

**Action tools:** Update records, trigger workflows, execute transactions. Like writing a prescription.

**Search tools:** Web search, internal knowledge base queries, documentation lookups. Like consulting UpToDate for the latest research.

The model doesn't inherently "know" how to use a database or send an email. The harness provides descriptions of available tools — what each does, what inputs it needs, what it returns. The LLM's reasoning ability ([Post 5](05-clinical-reasoning.md)) determines *when* to use which tool and *how* to interpret results.

This is where reasoning meets action. A model that can reason about your business context AND interact with your systems can automate workflows that previously required a human at every step — not because the individual steps were hard, but because they required judgment about *which* steps to take and in *what* order.

> **Simplification Note:** MCP (Model Context Protocol) is an emerging standard for how AI models connect to external tools and data sources. Think of it as a universal adapter — like USB-C for AI tools. MCP is gaining adoption but is still early. For now, tool connections are often custom-built per deployment.

*Deep dive: [Tool Use](Research_Docs/Terms/tool-use.md)*

---

## Trajectories: The Care Pathway

When a patient presents with symptoms, the doctor follows a **care pathway** — a sequence of steps unfolding over time, each informed by the results of the previous one.

*Initial assessment → order labs → review results → if abnormal, order imaging → consult specialist → develop treatment plan → monitor response → adjust*

This isn't a rigid script. If labs come back normal, the pathway branches differently. If a new symptom appears during treatment, the plan adjusts.

**Trajectories** describe the same concept for agents: the sequence of thoughts, decisions, tool calls, and actions an agent takes to accomplish a goal.

1. *Thought:* "The user wants Acme meeting prep. I need account information."
2. *Action:* Query CRM for Acme data.
3. *Observation:* 3-year customer, $200K ARR, last renewal flagged support concerns.
4. *Thought:* "Support concerns were flagged. Let me check recent tickets."
5. *Action:* Query support system for last 90 days.
6. *Observation:* 12 tickets, 3 escalated, 48-hour average resolution (above SLA).
7. *Thought:* "Check product usage to see if they're getting value despite support issues."
8. *Action:* Query analytics platform.
9. *Observation:* High core feature usage, low adoption of new features.
10. *Thought:* "Enough context. Synthesize a prep document addressing support proactively and highlighting adoption opportunities."
11. *Action:* Generate meeting prep document.

Each step is a decision. The agent didn't follow a predetermined script — it reasoned about what information it needed and adapted based on what it found.

**The RL Environment Stack** is how you build and evaluate these trajectories at enterprise scale:
- **Simulated Tools:** Sandboxed versions of your real systems for safe agent testing.
- **Realistic Data:** Production-representative data that captures the complexity of real workflows.
- **Long-Horizon Tasks + Rubrics:** Multi-step evaluation scenarios with scoring criteria designed by your domain experts.
- **Expert Network:** Your best people reviewing and scoring agent trajectories, creating the ground truth that makes the system better over time.

Domain-specific benchmarks like **BankerToolBench** (for financial services agent evaluation) demonstrate the principle: generic benchmarks tell you if an agent can use tools. Domain-specific benchmarks tell you if it can use tools *the way your best people would.* That's the evaluation gap most enterprises haven't closed.

> **Simplification Note:** Trajectory planning is one of the hardest problems in agent AI. Agents can get stuck in loops, take unnecessary steps, or miss efficient paths. The "LLM as a Judge" concept from [Post 4](04-board-exams.md) is increasingly used to evaluate agent trajectories, not just individual responses.

*Deep dive: [Trajectories](Research_Docs/Terms/trajectories.md)*

---

## Why This Matters for Your Organization

The human knowledge and evaluation layer is what makes enterprise agents trustworthy. Without it, you're in the >80% that see no EBIT impact. With it, you're building a force multiplier that compounds.

**Agents turn knowledge into action.** Everything earlier in this series — architecture, training, reasoning, knowledge base — converges here. An agent doesn't just know about your business. It *operates* within your business, using your tools, following your processes, acting on your data. This is where AI moves from 12 hours/week in time savings to fundamental operational transformation.

**Your processes are institutional knowledge too.** It's not just facts and documents. The *way* your organization does things — the sequence of steps in a deal approval, the criteria for escalating a support ticket, the process for onboarding a customer — becomes the agent's trajectory template. This is codified craftsmanship. The better documented your processes, the better your agents perform.

**Start at V1, not V4.** The most successful early deployments aren't fully autonomous. They're intelligent assistants handling multi-step research and preparation tasks, drafting communications for human review, or automating routine workflows with well-defined paths. Build trust at each level before advancing. Organizations that skip ahead join the 42% that abandon their initiatives.

**The harness determines the ceiling.** An agent is only as capable as the tools and systems it can access. Audit your tool landscape: what systems have APIs? What data is accessible programmatically? What actions can be triggered digitally? The more connected your infrastructure, the more capable your agents.

**Human oversight scales down over time, not immediately.** Think of agents like junior doctors: they start with heavy supervision and earn autonomy as trust is established. Deploy with human review on all outputs. Expand autonomous scope as confidence grows and edge cases are handled. The organizations achieving 3.7x quota attainment with AI aren't removing humans — they're making every human dramatically more effective, then gradually letting the system handle what it's proven it can do.

---

## Key Takeaway

Agents are LLMs that take action; harnesses provide the infrastructure enabling those actions; tool use extends capabilities into your real-world systems; and trajectories are the adaptive plans agents follow — with your institutional knowledge, documented processes, and expert evaluation serving as the ground truth that makes those trajectories intelligent, trustworthy, and aligned with how your organization actually works.

---

*Previous: [The Medical Library — RAG and Institutional Knowledge](08-the-medical-library.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
