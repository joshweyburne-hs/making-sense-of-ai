# Clinical Reasoning: How LLMs Think

*Part 5 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Reasoning, Chain of Thought, Inference
*For deeper technical dives on each term, see the [Term Reference Library](Research_Docs/Terms/).*

---

## The Problem

Most enterprise AI deployments stall at the simplest level: single-task automation. Summarize this email. Answer this FAQ. That's V0 on the maturity model, and it's where >80% of organizations plateau, seeing no meaningful EBIT impact from their AI investment. The reason? These tasks require recall, not reasoning. Real enterprise workflows demand multi-step thinking, weighing tradeoffs, and adapting when the situation changes. That's a fundamentally different capability, and it's the gap that separates demo-ready AI from production-ready AI.

---

## The Medical Scenario

A patient arrives in the emergency department with chest pain, shortness of breath, and a swollen left calf. A junior medical student immediately thinks "heart attack." An experienced physician sees the full picture differently.

*"Chest pain plus shortness of breath could be cardiac, but the swollen calf changes things. A swollen calf suggests DVT. A DVT can throw a clot to the lungs — a pulmonary embolism. Let me check D-dimer levels and order a CT pulmonary angiogram to confirm."*

That's differential diagnosis — systematic, step-by-step reasoning that separates great doctors from textbook memorizers. They don't pattern-match to the most obvious answer. They work through the logic, consider alternatives, weigh evidence, and arrive at a conclusion they can explain.

This kind of thinking is what separates modern LLMs from the chatbots of five years ago.

---

## Reasoning: System 1 vs. System 2

There's a fundamental difference between a search engine and a doctor. A search engine retrieves information. A doctor *reasons* with information: given these symptoms, this history, and these test results, what's the most likely diagnosis, and what should you do about it?

**Reasoning** in LLMs refers to the model's ability to go beyond retrieval and actually think through problems — connecting disparate information, following logical chains, making inferences, and arriving at conclusions that weren't in any single piece of training data.

**The paradigm shift of 2024-2026 is the System 1 / System 2 framework.** Think of it in medical terms:

**System 1 (fast, automatic):** A doctor glances at a rash and instantly says "shingles." No deliberation. Pattern recognition. Standard LLM token prediction works this way — fast, fluent, and often right for routine questions. But it's also where confident wrong answers come from.

**System 2 (slow, deliberate):** A doctor encounters a patient with contradictory symptoms, pulls out a whiteboard, and methodically works through differential diagnoses. This is analytical processing. The reasoning models that emerged in 2024-2025 — OpenAI's o1/o3, DeepSeek-R1, Claude with extended thinking — brought System 2 to LLMs. They can allocate more computational effort to harder problems, spending seconds on a simple question but minutes working through a complex proof.

The breakthrough wasn't just bigger models. It was training models to *think before answering.*

**Test-time compute scaling** makes this concrete. Instead of throwing more data or parameters at training (which has diminishing returns), you give the model more computation at inference time — when it actually needs to solve your problem. A 7B parameter model with extended deliberation can match a 70B model on complex reasoning tasks. You're trading speed for accuracy, exactly like a doctor taking five minutes on a complex case instead of thirty seconds on a routine one.

> **Simplification Note:** "Reasoning" in AI is a loaded term. Philosophers debate whether LLMs truly "reason" or simulate reasoning through sophisticated pattern matching. For practical purposes, what matters is the outcome: modern LLMs can work through multi-step problems and produce correct, useful answers. Whether that constitutes "real" reasoning doesn't change the value it delivers to your organization.

*Deep dive: [Reasoning](Research_Docs/Terms/reasoning.md)*

---

## Chain of Thought: Showing Your Work

In medical school, students are taught: "Never just give me the answer. Walk me through your reasoning." A student who says "pulmonary embolism" gets partial credit at best. A student who walks through the symptom pattern, risk factors, and differential demonstrates actual understanding.

**Chain of Thought (CoT)** is the AI equivalent. Instead of jumping to an answer, the model explicitly walks through its reasoning step by step.

Without CoT:
*"What is 17 times 23?"*
*"391"*

With CoT:
*"17 times 20 is 340. 17 times 3 is 51. 340 plus 51 is 391."*

This isn't cosmetic. When models "think step by step," accuracy on complex problems improves by 20-40 percentage points on math and logic tasks. The intermediate reasoning steps help the model arrive at better final answers.

**Process Reward Models (PRMs)** take this further. Instead of only rewarding the final answer (did you get the right diagnosis?), PRMs provide feedback on each reasoning step (was your differential logic sound? did you correctly weigh the risk factors?). This per-step feedback enables significantly better multi-step problem solving — the kind your enterprise workflows actually require.

The medical parallel is direct: the best diagnosticians don't think faster — they think more thoroughly. Chain of Thought gives LLMs this deliberative quality.

> **Simplification Note:** There are multiple flavors of CoT: few-shot (include reasoning examples in your prompt), zero-shot (simply say "think step by step"), and trained CoT (models specifically trained to reason internally, like o1 and DeepSeek-R1). RLVR (Reinforcement Learning from Verifiable Rewards) is used to train models to develop their own reasoning chains by rewarding correct final answers, letting the model discover effective reasoning steps itself.

*Deep dive: [Chain of Thought](Research_Docs/Terms/chain-of-thought.md)*

---

## Inference: The Moment of Diagnosis

Every piece of a doctor's training — med school knowledge, residency experience, clinical reasoning — converges in a single moment: the patient is in front of you, and you need a diagnosis and treatment plan. Right now.

That moment is **inference**. It's when the trained model is actually used — when it takes your input and generates an output. All the training is done. All the parameters are set. Now the model applies everything it learned to a new, real-world situation.

Every time you type a question into ChatGPT, Claude, or any LLM, you're triggering inference. The training happened weeks or months ago — inference is what happens in real time.

**It's probabilistic, not deterministic.** The model selects from probability distributions — not looking up stored answers. The same question asked twice might produce slightly different responses, just as two equally competent doctors might phrase the same diagnosis differently.

**More thinking = better answers (but slower and more expensive).** Test-time compute scaling means reasoning models can allocate more computation during inference on harder problems. The tradeoff is speed and cost. For your deployment decisions, this matters: a quick FAQ chatbot doesn't need deep reasoning. A complex deal-desk assistant analyzing multi-million-dollar contracts probably does.

**Inference quality depends on everything that came before.** Great architecture ([Post 1](01-the-blueprint.md)), trained on great data ([Post 2](02-medical-school.md)), refined through great feedback ([Post 3](03-residency.md)) — that's what produces great inference. It's the payoff of the entire training pipeline.

> **Simplification Note:** Inference also involves settings like "temperature" (how creative vs. deterministic), "top-p sampling" (which tokens are candidates), and "context management" (how conversation history is handled). These let you tune behavior at inference time without retraining — like adjusting how conservative a doctor should be in their diagnostic approach based on the clinical setting.

*Deep dive: [Inference](Research_Docs/Terms/inference.md)*

---

## Why This Matters for Your Organization

Reasoning is what separates V0 automation (single-task recall) from V1-V4 enterprise automation (multi-step workflows, complex decision-making, full process orchestration). Without reasoning, you have a search engine with a chat interface. With it, you have a force multiplier.

**Reasoning turns knowledge into problem-solving.** A model with access to your product documentation can answer factual questions. A model that can *reason* with your documentation can diagnose customer issues, recommend solutions to novel problems, and identify patterns across support tickets no individual agent would catch. That's where the 10-20% ROI uplift comes from.

**Chain of Thought builds trust.** When your AI recommends a specific product configuration, your sales team and your customers need to know *why.* A model that shows its reasoning — "Based on your requirements for X, Y, and Z, combined with your budget constraints, I recommend configuration A because..." — is far more trustworthy than one that outputs a recommendation with no explanation.

**Your institutional knowledge makes reasoning more valuable.** A model reasoning with generic internet knowledge reaches generic conclusions. A model reasoning with your competitive intelligence, your win/loss analyses, and your customer success patterns reaches conclusions uniquely valuable to your organization. The reasoning is the engine. Your codified craftsmanship is the fuel. That combination is your strategic moat.

**Inference cost is a real business consideration.** Understanding the tradeoff between reasoning depth and cost helps you make smart deployment decisions. Match the reasoning investment to the stakes of the decision.

---

## Key Takeaway

Reasoning gives LLMs the ability to think, not just recall; Chain of Thought makes that thinking explicit and dramatically improves accuracy; and inference is the real-time moment where all that training pays off — with the quality depending on everything that came before it, especially the institutional knowledge the model has to reason with.

---

*Previous: [Board Exams — Measuring What Models Know](04-board-exams.md)* | *Next: [Knowing What You Don't Know — Hallucination, Guardrails, and Grounding](06-knowing-what-you-dont-know.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
