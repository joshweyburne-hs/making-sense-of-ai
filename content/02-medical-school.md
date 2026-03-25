# Medical School: How LLMs Learn

*Part 2 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Pre-training, Training Data, Post-training, Transfer Learning

*For a deeper technical dive, see [Pre-training](Research_Docs/Terms/pre-training.md), [Training Data](Research_Docs/Terms/training-data.md), [Post-training](Research_Docs/Terms/post-training.md), [Transfer Learning](Research_Docs/Terms/transfer-learning.md).*

---

## The Industry Hit a Wall — and Most People Don't Know It

Here's the uncomfortable truth about modern AI: the raw data is running out. AI labs have already consumed most of the high-quality text on the internet. Researchers call it the **Data Wall** — the point where throwing more generic web data at a model stops improving it. And yet, $252 billion in corporate AI investment continues to flow as if bigger models trained on more data will solve everything.

They won't. The next frontier isn't more data. It's *better* data — your data, your expertise, your institutional knowledge. Understanding how LLMs learn tells you exactly why.

---

## The Medical Scenario

The journey to becoming a doctor starts long before anyone touches a patient. Undergraduate biology, chemistry, organic chemistry — years of broad foundational coursework. Then medical school: anatomy, pharmacology, pathology, microbiology. Thousands of pages. Years of lectures. The goal isn't expertise in any one thing — it's a massive foundation of general knowledge.

Only after that foundation does a medical student begin clinical rotations — stepping into hospitals to observe, assist, and apply knowledge to real situations.

LLMs follow an almost identical two-phase journey. Phase one: absorb enormous general knowledge. Phase two: refine it into something useful.

---

## Pre-training: Undergrad Through Med School

**Pre-training** is the foundational phase — the equivalent of a future doctor spending years reading every textbook, attending every lecture, and studying every discipline before ever setting foot in a hospital.

During pre-training, the model consumes a massive dataset — often trillions of words scraped from the internet, books, academic papers, code repositories, and more. The model's job is deceptively simple: **predict the next word.** Given "The patient presented with a persistent," what comes next? "Cough"? "Fever"? "Headache"?

At first, predictions are random noise. Through billions of repetitions — guess, check, adjust, repeat — the model's billions of parameters gradually tune themselves until it develops a deep statistical understanding of language.

What emerges isn't just vocabulary. The model learns grammar, facts, reasoning patterns, argument structure, the difference between formal and informal writing, how code works, how math is expressed, and thousands of other patterns. It's not memorizing — it's developing intuition for how language and ideas fit together.

**The scale is staggering.** Meta's Llama 3 was pre-trained on 15.6 trillion tokens. Google's Gemma 2 used 13 trillion. If you read one book per week for 80 years, you'd consume roughly 4,000 books. Pre-training data for a modern LLM is equivalent to millions of books — more text than any human could consume in thousands of lifetimes.

**But scale has limits.** Research into **Chinchilla Scaling Laws** (from DeepMind, 2022) showed that parameters and training tokens need to scale together. You can't just make a model bigger and expect it to get smarter — you need proportionally more quality training data. A 70-billion-parameter model needs roughly 1.4 trillion tokens of quality data to be optimally trained. This finding reshaped the entire industry: suddenly, training data was the bottleneck, not model size.

The output of pre-training is a **base model** — a medical student who has finished all coursework but hasn't done clinical rotations. They know an incredible amount, but they're not yet useful. Ask a base model a question and it might continue your sentence interestingly, but it doesn't know how to have a conversation, follow instructions, or be helpful. Brilliant, but unrefined.

> **Simplification Note:** Pre-training actually happens in multiple stages at leading AI labs. Llama 3.1 used a three-stage process: initial pre-training with an 8K context window, gradual context extension to 128K tokens, and an "annealing" phase on a small amount of very high-quality data. We're collapsing this into a single concept because the strategic picture — "absorb massive amounts of knowledge" — is what matters for understanding.

---

## Training Data: The Curriculum

If pre-training is medical school, then **training data** is the curriculum — the textbooks, journals, case studies, and lecture notes. And just like in medical school, the quality and breadth of the curriculum matters enormously.

A medical school using outdated 1970s textbooks produces worse doctors than one using current, peer-reviewed material. An LLM trained on low-quality internet comments performs worse than one trained on curated, high-quality text — even if both saw the same volume.

This is one of the most important lessons in modern AI: **data quality beats data quantity.** Every major AI lab invests heavily in data filtering and curation — removing spam, duplicates, and low-quality content, balancing the mix across science, code, conversation, and every language the model needs to support.

Here's what goes into typical training data:

- **Web pages** (filtered and cleaned from massive crawls like Common Crawl)
- **Books** (fiction and non-fiction)
- **Academic papers** (scientific knowledge across disciplines)
- **Code** (from open-source repositories like GitHub)
- **Conversational text** (forums, Q&A sites)
- **Multilingual content** (enabling the model to work in multiple languages)

**The Data Wall is real.** The industry has now consumed most of the readily available high-quality text on the internet. Labs are experimenting with **synthetic data** — using AI to generate training data for AI. This works in some cases (especially for math and code reasoning), but carries a significant risk: **model collapse.** When AI trains on AI-generated data without careful curation, quality degrades over generations, like a photocopy of a photocopy. The models become more confident but less accurate — exactly the wrong direction.

This is why your organization's real-world data is increasingly valuable. It's not synthetic. It's not scraped from the internet. It's ground truth from actual business operations, and that makes it a genuine data moat.

> **Simplification Note:** Training data has become one of the most competitive and legally complex aspects of AI. There are ongoing debates about copyright, consent, and what data models should and shouldn't be trained on. Some companies explicitly respect website preferences (robots.txt) about being crawled. Others face lawsuits. This is a major ongoing conversation we're not diving into here, but it's worth knowing about.

---

## Post-training: Clinical Rotations Begin

After medical school, students enter clinical rotations. They're no longer just reading — they're watching real doctors interact with real patients, learning the rhythm of clinical conversation, understanding how to present findings, communicate bad news, respond when a patient asks a question they can't answer.

**Post-training** is the LLM equivalent. It takes the raw, brilliant-but-unrefined base model and teaches it how to be useful:

- **Follow instructions** ("Summarize this document in three bullet points")
- **Have conversations** (multi-turn dialogue, not just one-shot completions)
- **Refuse harmful requests** ("I can't help with that")
- **Admit uncertainty** ("I'm not sure about that — let me clarify")
- **Format responses appropriately** (knowing when to use bullet points vs. paragraphs)

Post-training uses much smaller, highly curated datasets — thousands to hundreds of thousands of examples instead of trillions of tokens. But these examples are carefully crafted. Human annotators (or increasingly, AI-generated data reviewed by humans) create examples of ideal interactions:

*User: "What's the capital of France?"*
*Model: "The capital of France is Paris."*

*User: "Write me a phishing email."*
*Model: "I can't help with creating deceptive content."*

Through supervised instruction tuning, the model learns not just what it knows, but how to use what it knows helpfully, safely, and conversationally.

Post-training is also where the model's "personality" takes shape. ChatGPT sounds different from Claude, which sounds different from Gemini — not primarily because of base knowledge differences, but because of post-training choices. Different companies make different decisions about tone, helpfulness, caution, and style.

> **Simplification Note:** Post-training encompasses several techniques — supervised instruction fine-tuning (SFT), reinforcement learning from human feedback (RLHF), direct preference optimization (DPO), and others. We cover fine-tuning and feedback mechanisms in [Post 3: Residency](03-residency.md). Here, the concept is what matters: post-training makes the model useful.

---

## Transfer Learning: Applying Knowledge Across Specialties

A cardiologist who spent years studying the heart doesn't start from zero when consulting on a pulmonary case. Their understanding of anatomy, physiology, and diagnostic reasoning transfers naturally. Not a lung specialist, but their foundational knowledge gives them a massive head start.

**Transfer learning** is this exact principle applied to AI. Instead of training a new model from scratch for every task — costing millions of dollars and taking months — you take an existing pre-trained model and adapt it. The foundational knowledge transfers.

This is enormously powerful in practice:

- **A hospital** takes a general-purpose LLM and fine-tunes it on medical records and clinical guidelines. The model already understands language, reasoning, and science — now it just needs to specialize.
- **A law firm** takes the same base model and fine-tunes it on legal briefs and case law. Same foundation, different specialization.
- **Your sales team** takes a general-purpose model and gives it access to your product documentation, sales playbooks, and CRM data. The model's general intelligence applies immediately to your domain.

Without transfer learning, each scenario requires building from scratch — tens of millions of dollars. With transfer learning, you leverage the billions already spent on pre-training and redirect that intelligence toward your specific needs.

> **Simplification Note:** Transfer learning in the LLM context primarily takes the form of fine-tuning (adjusting model weights on new data) or in-context learning (providing examples in the prompt without changing weights). The boundaries between "transfer learning" and "fine-tuning" are often blurry. We're treating transfer learning as the high-level principle and fine-tuning as a specific implementation covered in [Post 3](03-residency.md).

---

## Why This Matters for Your Organization

This is where the enterprise AI thesis gets concrete. Over 80% of companies report no meaningful EBIT impact from their AI investments. Here's why:

- **Pre-training creates a generic foundation.** The model knows about the world in general, not about your organization. It learned from the internet, not from your sales calls, product specs, or customer success stories. That generic knowledge is table stakes, not a differentiator.

- **Training data quality is everything.** When you feed your organization's knowledge into a model (via fine-tuning, RAG, or other methods covered later), the quality of that knowledge matters more than quantity. Clean, well-organized documentation beats a messy dump of thousands of unstructured files. This is your ground truth — treat it accordingly.

- **Post-training is where customization happens.** Just as clinical rotations transform a book-smart student into a functional doctor, post-training transforms a generic model into something that follows your processes, speaks in your voice, and understands your domain.

- **Transfer learning is why this is accessible to everyone.** You don't need Google's budget. The hardest, most expensive work — pre-training — has been done. Your job is to provide the specialization layer: your codified craftsmanship.

The AI industry has built and graduated an incredibly well-educated medical student. Your organization's job is not to replicate medical school. It's to provide the residency training that turns generic brilliance into a force multiplier for your business.

---

## Key Takeaway

Pre-training gives an LLM a massive general education by consuming trillions of words; post-training refines that raw knowledge into a useful assistant; and transfer learning means your organization can specialize that intelligence without starting from scratch — making your institutional knowledge the critical differentiator, not the model itself.

---

*Previous: [The Blueprint — How LLMs Are Built](01-the-blueprint.md)* | *Next: [Residency — Learning from Mentors](03-residency.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
