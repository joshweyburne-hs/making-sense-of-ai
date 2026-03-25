# Residency: Learning from Mentors

*Part 3 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Supervised Fine-tuning, Reinforcement Learning, RLHF, Alignment

*For a deeper technical dive, see [Supervised Fine-tuning](Research_Docs/Terms/supervised-fine-tuning.md), [Reinforcement Learning](Research_Docs/Terms/reinforcement-learning.md), [RLHF & Alignment Techniques](Research_Docs/Terms/rlhf-and-alignment-techniques.md), [Alignment](Research_Docs/Terms/alignment.md).*

---

## 42% of AI Initiatives Fail. This Is Why.

Models learn from the average, not the best. Pre-training absorbs the internet — a mix of brilliance and noise in roughly equal measure. Without expert human feedback, your AI reflects the median of the web, not the top performers in your organization.

That's why 42% of companies abandoned their AI initiatives last year. Not because the models lacked capability — because nobody built the feedback loops to teach them what "good" looks like in their specific context. The residency phase is where that problem gets solved. And it's the phase most enterprises skip.

---

## The Medical Scenario

Medical school is over. The newly minted doctor knows an extraordinary amount — but they've never been responsible for a patient. Residency changes everything. Now they're in the hospital, making decisions under the watchful eye of experienced attending physicians who correct diagnoses, challenge reasoning, and shape judgment through thousands of real-world interactions.

A resident doesn't just learn *what* to do. They learn *how* — the tone with anxious families, the instinct for when a case needs escalation, the judgment to know when "by the book" isn't enough. This refinement comes not from textbooks but from feedback: do this, not that. This answer was better than that one. This approach is safer.

LLMs go through their own residency. And like medical residency, it's the feedback loop — not the foundational knowledge — that transforms a smart-but-raw model into something genuinely useful and trustworthy.

---

## Supervised Fine-tuning: The Attending Shows You How

In the first weeks of residency, an attending physician demonstrates. They show the resident exactly how to present a case, structure a treatment plan, document findings. "When you see this, do this. Here's how I would have handled that."

**Supervised Fine-tuning (SFT)** works the same way. Human trainers (or increasingly, AI systems reviewed by humans) create thousands of example interactions that show the model exactly how to respond:

*Input:* "Explain photosynthesis in simple terms."
*Desired Output:* "Photosynthesis is how plants make food using sunlight. They absorb light through their leaves, take in carbon dioxide from the air and water from the soil, and convert these into glucose (sugar) for energy. Oxygen is released as a byproduct — which is what we breathe."

The model sees thousands of these examples and adjusts its parameters to produce responses that match — helpful, clear, appropriately detailed, honest about limitations.

SFT is remarkably effective at teaching *format and style*. Before SFT, a base model might respond to "What's the capital of France?" with a Wikipedia-style essay. After SFT, it gives a direct, conversational answer. It learns when to use bullet points, how long responses should be, and when to ask clarifying questions.

Think of SFT as the "monkey see, monkey do" phase. The resident watches the attending handle 500 cases and internalizes the patterns. Powerful, but limited: it can only teach the model to mimic what was demonstrated. It doesn't teach the model to *judge* between two approaches when neither was shown.

> **Simplification Note:** SFT includes several technical variants — full fine-tuning (updating all parameters), LoRA/QLoRA (updating only a small subset for efficiency), and instruction tuning (a specific form focused on following instructions). For most business conversations, these distinctions matter less than the core concept: you show the model examples of good behavior, and it learns to replicate them.

---

## Reinforcement Learning: Learning from Outcomes

As a resident gains experience, learning shifts. They're no longer just copying the attending — they're making their own decisions and observing consequences. A patient improves: positive signal. A diagnosis turns out wrong: negative signal. Over hundreds of cases, clinical intuition develops not from being *shown* what to do, but from seeing the *results* of their choices.

**Reinforcement Learning (RL)** applies this feedback-driven learning to models. Instead of being shown the "correct" answer, the model generates responses and receives a reward signal — a score — based on quality. Over thousands of iterations, the model learns to produce responses that maximize this reward.

The core loop:
1. The model generates a response
2. The response receives a score (reward)
3. The model adjusts to produce higher-scoring responses next time

This is fundamentally different from SFT. SFT says "here's the right answer, copy it." RL says "try something, and I'll tell you how good it was." RL can discover approaches that no one explicitly demonstrated — just as a resident might develop diagnostic intuition their attending never explicitly taught.

The challenge: defining the reward. In chess, the reward is clear — win or lose. In language? What makes one response "better" than another? This is where RLHF comes in.

> **Simplification Note:** Reinforcement Learning is a broad field predating LLMs by decades — behind AlphaGo, self-driving car training, and robotic control. In the LLM context, RL is specifically used during post-training to refine behavior based on feedback signals. We're focused on the LLM application, not the full breadth of RL.

---

## RLHF: The Human Element

Here's where the medical analogy gets especially resonant — and where the enterprise AI thesis gets sharp.

The best doctors don't just have knowledge and clinical skills. They have bedside manner. They know how to explain a diagnosis so a worried parent understands. They know the difference between a technically correct answer and a *helpful* one.

This judgment is hard to teach through examples alone. It comes from feedback — patient reactions, peer review, colleagues saying "your answer was correct, but the delivery could have been better."

**Reinforcement Learning from Human Feedback (RLHF)** teaches LLMs this nuanced judgment:

**Step 1: Generate multiple responses.** The model answers a question several ways.

**Step 2: Humans rank the responses.** Human evaluators rank them from best to worst — based on judgment about helpfulness, accuracy, safety, and tone.

**Step 3: Train a reward model.** These preferences train a separate "reward model" that learns to predict which responses humans would prefer. This acts as a proxy for human judgment, allowing the system to scale.

**Step 4: Optimize the main model.** The original model is fine-tuned using RL, with the reward model providing the reward signal.

**Human expertise is now the bottleneck.** Credentialed annotators who can evaluate domain-specific outputs cost $50-250/hr — more expensive than the compute they're training. This is why RLHF at scale is harder than pre-training: compute you can buy; expertise you have to find, hire, and retain. For your organization, this means the experts who can judge AI quality in your domain are your scarcest and most valuable resource.

RLHF is what made ChatGPT feel different from previous chatbots. The underlying GPT model was powerful before RLHF, but it didn't *feel* helpful. It rambled, gave overly technical answers, produced content that was technically accurate but contextually wrong. RLHF taught it to be a conversationalist humans actually enjoy interacting with.

> **Simplification Note:** RLHF is one of several preference-tuning techniques, and the spectrum is expanding rapidly.
>
> **Direct Preference Optimization (DPO)** achieves similar results without training a separate reward model — it optimizes directly on human preference pairs. DPO is simpler, more stable, and increasingly popular. Meta used it for Llama 3. Many organizations are adopting it because it's less infrastructure-heavy than full RLHF while delivering comparable alignment quality. If RLHF is a full residency program with attending oversight, DPO is a structured peer-review system that achieves the same refinement with less overhead.
>
> **ORPO (Odds Ratio Preference Optimization)** combines instruction tuning and preference alignment in a single training step, eliminating the need for a separate SFT phase. It's more compute-efficient and showing strong results for smaller organizations.
>
> **GRPO (Group Relative Policy Optimization)** takes a different approach entirely — it generates multiple responses and uses the group's relative quality to compute rewards, removing the need for a reward model altogether. DeepSeek used GRPO for their R1 reasoning model.
>
> **RLVR (Reinforcement Learning from Verifiable Rewards)** works for math and code where correctness can be checked automatically. The industry hasn't settled on a single best approach — different labs use different methods, often combining multiple techniques. What matters conceptually: all these methods serve the same purpose — teaching the model what "good" looks like based on feedback, not just examples.

---

## Alignment: Medical Ethics for AI

Every medical school has an ethics curriculum. Doctors learn "do no harm," patient autonomy, informed consent, the boundaries of practice. A surgeon who *could* perform a risky procedure but *shouldn't* given the patient's wishes — that's ethics shaping behavior even when capability exists.

**Alignment** is the AI equivalent. It's the umbrella term for ensuring a model's behavior matches human values and intentions. An aligned model:

- Helps users accomplish goals without causing harm
- Refuses requests that would cause damage (even if it *could* fulfill them)
- Is honest about limitations rather than fabricating
- Treats users fairly without harmful biases
- Follows the spirit of an instruction, not just the letter

Alignment isn't a single technique — it's a goal that SFT, RLHF, DPO, and other methods all contribute to. Think of it as the overarching principle guiding all "residency" training: not just making the model smart or helpful, but making it *trustworthy.*

This is harder than it sounds. Too cautious, and the model refuses benign questions about chemistry out of misuse concerns. Not cautious enough, and it cheerfully provides harmful instructions. Finding the right balance is one of the most active areas of AI research.

The stakes are real. An unaligned model deployed in a customer-facing role could provide dangerous advice, fabricate product capabilities, or behave in ways that damage your brand. Alignment is what stands between a powerful model and a trustworthy one.

> **Simplification Note:** Alignment is deeply debated. Some researchers focus on near-term alignment (making current models helpful and safe), others on long-term alignment (ensuring future superintelligent AI remains beneficial). This series focuses entirely on near-term, practical alignment — the kind that determines whether your AI assistant gives good answers and refuses harmful ones.

---

## Why This Matters for Your Organization

The residency phase is where institutional knowledge becomes actionable — and where most enterprises leave value on the table:

- **SFT is how you teach a model YOUR way of doing things.** If your best sales reps have a specific discovery methodology, you can create training examples that demonstrate it. The model learns to mimic your experts, not generic internet advice. This is **codified craftsmanship** — turning tribal knowledge into a scalable asset.

- **RLHF / preference tuning captures judgment that's hard to write down.** Some institutional knowledge isn't in documents — it's in the instinct of a 20-year veteran who "just knows" which approach to take. By having experienced team members rank model outputs, you capture and scale that judgment. Organizations that implement this human-in-the-loop approach report **3.7x quota attainment** and **12 hours/week in time savings** when AI becomes a true force multiplier for their teams.

- **Alignment determines trust.** Before deploying AI to interact with your customers, partners, or internal teams, you need confidence it represents your organization appropriately. Alignment ensures the model stays within your brand guidelines, compliance requirements, and ethical standards.

- **The feedback loop never ends.** Just as doctors continue learning through peer review and continuing education, the best AI deployments include ongoing feedback mechanisms. Users flag bad responses. Subject matter experts review edge cases. The model improves as your organization's feedback compounds.

The most valuable models aren't the ones with the most parameters. They're the ones refined through the highest quality feedback from the people who know your business best. Your expert judgment is the strategic moat. Everything else is a commodity.

---

## Key Takeaway

Supervised fine-tuning teaches a model *what* to do by showing examples; reinforcement learning teaches it *how* to improve through feedback; RLHF adds the human judgment that separates technically correct from genuinely helpful; and alignment ensures all of this produces behavior you can trust — just as residency transforms a book-smart graduate into a doctor you'd trust with your family.

---

*Previous: [Medical School — How LLMs Learn](02-medical-school.md)* | *Next: [Board Exams — Measuring What Models Know](04-board-exams.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
