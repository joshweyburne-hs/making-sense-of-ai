# The Blueprint: How LLMs Are Built

*Part 1 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** LLM Architecture, Transformers & Attention, Weights & Parameters, Tokenization

*For a deeper technical dive, see [LLM Architecture](Research_Docs/Terms/llm-architecture.md), [Transformers & Attention](Research_Docs/Terms/transformers-and-attention.md), [Weights & Parameters](Research_Docs/Terms/weights-and-parameters.md), [Tokenization](Research_Docs/Terms/tokenization.md).*

---

## You Can't Evaluate What You Don't Understand

Every vendor in your inbox claims their AI is "best-in-class." Most of them are wrong — or at least, wrong for your use case. The only way to avoid being sold the wrong solution is to understand what you're buying at the architectural level.

You don't need to build an LLM. But you need to understand the blueprint. Just like a physician doesn't build a brain, but understanding neuroanatomy makes everything else in medicine click — understanding LLM architecture makes every other AI decision in your organization sharper.

---

## The Medical Scenario

Before a medical student ever touches a patient, they study anatomy. Billions of neurons connected by synapses, organized into regions handling vision, language, movement, memory. They don't need to build a brain. But they need to understand its blueprint.

LLMs have a blueprint too. And understanding it makes every other concept in this series fall into place.

---

## LLM Architecture: The Brain's Structure

A human brain has roughly 86 billion neurons organized into layers and regions, each with a role. The visual cortex processes what you see. Broca's area handles speech. The prefrontal cortex manages reasoning.

An LLM is organized the same way — in layers. Information enters at the bottom, passes through dozens (sometimes over a hundred) layers of processing, and emerges at the top as a response. Each layer transforms the information, adding understanding and nuance.

When someone says "GPT-4" or "Claude" or "Llama," they're referring to a specific architecture — a specific arrangement of these layers. Like comparing the brain of a human to the brain of a dolphin. Both impressive. But the wiring is different, and that wiring determines capability.

The dominant architecture behind virtually every modern LLM is the **Transformer**, introduced in 2017 in a paper titled "Attention Is All You Need." Before Transformers, AI models read text one word at a time, left to right. Transformers changed everything by enabling the model to look at an entire passage simultaneously.

> **Simplification Note:** We're describing a "decoder-only" Transformer, which is what GPT, Claude, and most modern LLMs use. The original 2017 paper described an "encoder-decoder" architecture used for translation. Some models like Google's T5 still use that design. For this series, when we say "Transformer," we mean the decoder-only variant that powers today's chatbots and assistants.

---

## Transformers & Attention: Focusing on What Matters

A patient walks into the ER: *"Three-day headache, blurry vision, bad sushi last week, sore knee from hiking, and a family history of aneurysms."*

A first-year student gets lost in the noise. An experienced physician immediately zeros in: **three-day headache + blurry vision + family history of aneurysms.** That combination matters. Everything else is background.

This is exactly what the **Attention Mechanism** does inside a Transformer. When processing text, the model calculates how much "attention" every word should pay to every other word. Some relationships matter enormously. Others don't.

Consider: *"The doctor told the nurse that she needed to review the patient's chart before the surgery."*

Who does "she" refer to? Humans resolve this instantly through context. The Attention Mechanism does the same thing mathematically, assigning high attention scores between "she" and the most relevant noun based on patterns learned during training.

This ability to focus on what's relevant — across an entire passage, all at once — is why Transformers were a breakthrough. Previous models processed text sequentially and "forgot" important details from earlier in a passage. Transformers connect a word at the beginning of a document to a word at the end, if the relationship matters.

> **Simplification Note:** The actual mechanism involves mathematical constructs called Query, Key, and Value matrices. Each word "asks a question" (Query), every other word "advertises what it contains" (Key), and the model retrieves the relevant information (Value). Modern LLMs also use "Multi-Head Attention" — multiple attention processes in parallel, each looking for different types of relationships (grammar, meaning, sentiment). We're skipping the math because the concept is what matters for your purposes.

---

## Weights & Parameters: Billions of Tuning Dials

If the Transformer architecture is the brain's structure, then **parameters** are the strength of every neural connection.

A brand-new piano has 88 keys, perfectly built. But it means nothing until a tuner adjusts thousands of internal components — string tension, hammer alignment, damper responsiveness — so that pressing a key sounds right.

An LLM's parameters work the same way. Billions of numbers, each a tiny dial adjusted during training. When someone says "GPT-4 has 1.76 trillion parameters," they mean 1.76 trillion adjustable dials, each set to a precise value like 0.5473 or -0.8291.

**Weights** are the most important type of parameter. They control how strongly one piece of information influences another as it flows through the model's layers. High weight between two concepts means the model learned they're strongly connected. Low weight means they're not.

Nobody manually sets these values. During training, the model starts with random parameter values and adjusts them trillions of times based on examples. Like learning to ride a bike — thousands of micro-adjustments until balance clicks.

Here's the part that surprises most people: **no one fully understands what individual parameters do.** Scientists can't point to parameter number 45,729,483 and say "this one handles French grammar." The knowledge is distributed across millions of parameters in complex patterns. The models work remarkably well — but explaining exactly why a specific parameter has a specific value is still an open research question.

**What the numbers mean for you:** Parameter count gives you a rough sense of capacity. A 7-billion-parameter model is like a well-read general practitioner. A 70-billion-parameter model is like a specialist with deeper knowledge. A 700-billion+ parameter model is like having an entire medical department. More parameters means more room to store knowledge — but only if that capacity was filled with quality training data (covered in [Post 2: Medical School](02-medical-school.md)).

> **Simplification Note:** Parameters also include "biases" (baseline values that shift outputs) and other learned values beyond just weights. We're grouping them all under "parameters" because the distinction rarely matters in conversation. The relationship between parameter count and capability isn't perfectly linear — a well-trained 7B model can outperform a poorly trained 70B model. Architecture and training quality matter as much as size. Techniques like "Mixture of Experts" (MoE) allow models to have hundreds of billions of total parameters while only activating a fraction for any given input — like having 256 specialist doctors on staff but only consulting the 8 most relevant ones per patient.

---

## Tokenization: How the Model Reads

Before a medical student can learn from textbooks, they need the language of medicine. "Myocardial infarction" needs to become a recognizable unit — not seven confusing syllables, but one concept: heart attack. Medical students build a vocabulary that lets them process information efficiently.

LLMs do something similar through **tokenization** — breaking text into digestible pieces called "tokens."

The twist: tokens aren't always whole words.

- "understanding" → ["under", "standing"]
- "cardiologist" → ["card", "iol", "ogist"]
- "the" → ["the"]
- "AI" → ["AI"]

Common words stay whole. Uncommon words get split. The model learns a vocabulary of roughly 50,000-100,000 token pieces that combine to represent virtually any text.

**Why this matters in practice:** Tokenization is why you hear about "token limits" and "cost per token." When an LLM processes your input or generates a response, it works in tokens, not words. A typical English word averages about 1.3 tokens. A 1,000-word document is roughly 1,300 tokens.

This connects directly to **context windows** (covered in [Post 7: The Patient Chart](07-the-patient-chart.md)) — the maximum number of tokens a model can process at once. A "128K context window" means roughly 128,000 tokens — about a 300-page book.

> **Simplification Note:** There are multiple tokenization approaches (Byte-Pair Encoding, WordPiece, SentencePiece), each with different strategies for splitting text. Different models use different tokenizers, which is why the same text might cost different token counts on different platforms. We're treating tokenization as a single concept because the differences between methods rarely matter for business conversations.

---

## Why This Matters for Your Organization

$252 billion is flowing into AI. The wrong architectural choice wastes your share of that investment. Understanding the blueprint helps you ask the right questions:

- **Architecture choice** determines what kinds of tasks a model excels at. Not all LLMs are built the same way, and the architecture affects how well it absorbs and uses your organization's knowledge.

- **The Attention Mechanism** is why modern LLMs can process your 50-page product manual and pull out the one paragraph that answers a customer's specific question. It's the mechanism that makes institutional knowledge *usable* at scale.

- **Parameter count** gives you a mental model for capacity, but it's not the whole story. A smaller model fine-tuned on your organization's data can outperform a larger generic model for your specific use cases — just like a community physician who knows every patient by name often provides better care than a world-famous specialist who's never met them.

- **Tokenization** affects cost and what fits in the model's working memory. When you're deciding how much of your knowledge base to feed into a model, you're making decisions in tokens.

The model is not your strategic moat. Understanding it well enough to deploy it correctly is.

---

## Key Takeaway

An LLM is a layered processing system (architecture) that learned to focus on what matters (attention) by adjusting billions of internal settings (parameters) to process language broken into small pieces (tokens) — and understanding this blueprint is the foundation for everything else in this series, just as anatomy is the foundation for everything in medicine.

---

*Next: [Medical School — How LLMs Learn](02-medical-school.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
