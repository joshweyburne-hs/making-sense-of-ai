# The Patient Chart: Context, Memory, and Communication

*Part 7 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Context Windows, Memory, Prompt Engineering
*For deeper technical dives on each term, see the [Term Reference Library](Research_Docs/Terms/).*

---

## The Problem

Thirty-eight percent of enterprises say their data isn't ready for AI. That's not a model problem or a compute problem — it's a context management problem. Your organization's knowledge exists in scattered documents, email threads, tribal knowledge, and systems that don't talk to each other. The AI can't use what it can't see, and how you present what it *can* see determines whether you get a force multiplier or an expensive autocomplete.

---

## The Medical Scenario

A hospitalist takes over a complex patient at shift change. Fifteen minutes to review the chart before rounds. The patient has been in the hospital for a week with multiple complications. The chart is 200 pages.

The doctor can't read all 200 pages. So they prioritize: the most recent attending notes, today's labs, the current medication list, the last specialist consultation. They skim the admission summary for context. They skip the routine nursing vitals from three days ago.

Then comes the handoff. How the outgoing doctor presents the case matters enormously.

**Resident A:** *"So this patient came in and they had some chest pain and they've been taking medications and they have a history of stuff and their labs showed some things..."*

**Resident B:** *"58-year-old male, day 7, admitted for community-acquired pneumonia complicated by AKI, currently on IV antibiotics with improving renal function, key concern today is..."*

Same patient. Dramatically different outcomes based on what's included and how it's presented. Both of these — what fits in the chart review and how the case is communicated — have direct parallels in how LLMs work.

---

## Context Windows: How Much the Doctor Can Read at Once

Every LLM has a **context window** — the maximum amount of text it can "see" at one time. Think of it as the size of the patient chart the doctor can hold in working memory during a single encounter.

Context windows are measured in tokens (the text fragments from [Post 1](01-the-blueprint.md)):

- **Early models (2022):** ~4,000 tokens (~3,000 words) — a single page of chart notes
- **GPT-4 (2023):** ~128,000 tokens (~96,000 words) — a short book
- **Frontier models (2025-2026):** 200,000 to 1,000,000+ tokens — several full-length novels
- **Experimental models:** Gemini and Llama 4 Scout have pushed to 10 million tokens — an entire medical school textbook library

This expansion has been dramatic. In 2022, you could barely fit a long email. Today, you can feed in an entire codebase, a full legal contract, or months of customer support transcripts.

**But bigger isn't always better.** A doctor with a 200-page chart and 15 minutes doesn't benefit from being given a 2,000-page chart. More information helps only if it's relevant and well-organized. The same is true for LLMs: stuffing a million tokens with irrelevant information doesn't produce better answers. It can produce *worse* answers, because the model has to find the needle in a much larger haystack.

Research shows LLMs exhibit a "lost in the middle" effect — they pay more attention to information at the beginning and end of their context window, missing details buried in the middle. Strikingly similar to how you skim long documents, anchoring on the opening and conclusion.

> **Simplification Note:** Context window size is one of the most marketed specs in AI, but effective utilization matters more than raw size. A 200K window used well often outperforms a 1M window with poor focus. Longer context also means higher cost. For most business applications, the question isn't "how big is the context window?" but "are you putting the right information in it?"

*Deep dive: [Context Windows](Research_Docs/Terms/context-windows.md)*

---

## Memory: Remembering Across Visits

A great family physician remembers that Mrs. Johnson is allergic to penicillin, had a knee replacement last year, and is anxious about her daughter's upcoming surgery. They don't re-read her entire chart before every visit — they *remember.*

LLMs have an analogous split:

**In-context memory (short-term):** Everything within the current context window. When ChatGPT remembers what you said five messages ago, the entire conversation is sitting in the context window. When the conversation ends or exceeds the window, that memory vanishes unless specifically saved.

**Persistent memory (long-term):** Newer systems store and retrieve information across conversations:
- **Conversation summaries** automatically included in future sessions.
- **User profiles** with preferences and context that persist across sessions.
- **External memory stores** the model can query to "remember" past interactions.

The distinction shapes your deployment decisions. An LLM without persistent memory treats every conversation as its first — like a locum tenens doctor who's never met the patient. An LLM *with* persistent memory builds on past interactions — like a long-term primary care physician who knows your history.

The challenge is curation. A doctor doesn't need to remember every detail of every visit for 20 years. They need to remember what's *relevant.* The best AI memory systems are selective — storing important context and discarding noise.

> **Simplification Note:** "Memory" in AI covers a wide spectrum — from simple conversation history stored as text, to vector databases with semantically searchable memories, to the model's own parameters (learned memory from training). The specifics vary across products and platforms.

*Deep dive: [Memory](Research_Docs/Terms/memory.md)*

---

## Prompt Engineering: The Art of the Case Presentation

In medicine, a "good presentation" is an art form. A well-presented case gives the attending exactly the information they need, in the right order, to make good decisions quickly.

**Prompt engineering** is the skill of presenting information to an LLM in a way that produces the best possible output. Not tricks or magic words — clear, structural communication.

**Be specific about what you want.** "Tell me about our product" produces a vague response. "Summarize the three key differentiators of our Enterprise product vs. competitors, as bullet points with one sentence each" produces something useful.

**Provide relevant context.** "What should I say to this customer?" is worse than "This customer is a mid-market healthcare company evaluating us against Competitor X. They're concerned about implementation time. What should I say?" Context changes everything, just as patient history changes a diagnosis.

**Assign a role or perspective.** "You are a senior sales engineer with 10 years of experience in healthcare IT" often produces more relevant responses than a generic prompt.

**Show the format you want.** If you want a bulleted summary, show an example. Models are excellent at matching demonstrated patterns.

**Iterate.** The first prompt rarely produces the perfect result. Just as a doctor refines their assessment as new information comes in, prompt engineering is often a conversation.

> **Simplification Note:** Prompt engineering has generated an entire cottage industry of guides and courses. The fundamentals are straightforward: be clear, provide context, specify desired output, and iterate. Advanced techniques like few-shot prompting, system prompts, and structured output formatting build on these basics.

*Deep dive: [Prompt Engineering](Research_Docs/Terms/prompt-engineering.md)*

---

## Why This Matters for Your Organization

That 38% data-readiness gap is a context management problem in disguise. Solve it, and you're ahead of most of your competitors.

**Context window management is strategic.** You can't dump your entire knowledge base into a prompt and hope for the best. Smart curation — selecting the most relevant documents, ordering them thoughtfully, summarizing where appropriate — dramatically improves output quality. The people who know your business best are the best curators.

**Memory transforms one-off interactions into relationships.** A customer-facing AI that remembers past interactions, preferences, and history provides fundamentally better service than one that starts fresh every time. Building memory into your AI systems is building institutional knowledge into every interaction.

**Prompt engineering is the new business communication skill.** Just as "how to write a good email" became a core professional skill, "how to communicate effectively with AI" is becoming one. The sales rep who can clearly articulate context, constraints, and desired outcomes will get dramatically better results — and that skill compounds across your entire team. Research shows 3.7x quota attainment for sales reps who effectively partner with AI tools, with 12 hours per week in time savings.

**The combination is multiplicative.** Good institutional knowledge (the right context), presented effectively (prompt engineering), with relevant history (memory), within appropriate limits (context window) — this combination separates an AI deployment that transforms productivity from one that generates shrugs and eye-rolls.

---

## Key Takeaway

The context window is how much information a model can work with at once; memory extends that across conversations; and prompt engineering is the skill of presenting information effectively — together, they determine whether your institutional knowledge actually reaches the model in a form it can use.

---

*Previous: [Knowing What You Don't Know — Hallucination, Guardrails, and Grounding](06-knowing-what-you-dont-know.md)* | *Next: [The Medical Library — RAG and Institutional Knowledge](08-the-medical-library.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
