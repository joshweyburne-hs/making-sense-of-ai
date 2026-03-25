# Context Windows

Context windows define how much information an LLM can see and process at one time. They are the model's working memory: everything the model considers when generating its next token must fit within this fixed-size window.

## How It Works

A context window is measured in tokens, roughly three-quarters of a word each. Early transformer models (GPT-3, 2020) had context windows of 2,048-4,096 tokens, roughly 3-6 pages of text. This was a hard architectural constraint: the self-attention mechanism at the core of transformers computes relationships between every pair of tokens in the window, and the computational cost scales quadratically with window size.

The evolution has been dramatic. GPT-4 (2023) pushed to 128K tokens. Claude expanded to 200K. Gemini 1.5 reached 1 million tokens in early 2025, and models entering 2026 are pushing beyond that. Architectural innovations like sliding window attention, sparse attention patterns, and ring attention broke through the quadratic scaling barrier, making million-token contexts computationally feasible.

But bigger is not always better. Research consistently demonstrates the "lost in the middle" effect: models pay strong attention to information at the beginning and end of their context window but lose track of material buried in the middle. A 1-million token context window stuffed with documents does not mean the model actually uses all that information effectively. Retrieval precision often degrades as context length increases because the signal-to-noise ratio drops.

Quality of context management matters more than raw window size. A well-curated 8K-token context with precisely relevant information consistently outperforms a 128K-token context filled with marginally related documents. This is why RAG systems that retrieve the most relevant passages, rather than dumping entire document collections, produce better results despite using a fraction of available context.

Cost is directly proportional to context usage. You pay per input token processed and per output token generated. A 100K-token context costs roughly 25x more than a 4K-token context per query. For enterprise applications running thousands of queries per day, the difference between efficient context management and context stuffing is the difference between viable and ruinously expensive.

## Medical Analogy

The context window is the patient chart the physician has open during a consultation. A 4K-token window is like reading a single page of notes. A 128K-token window is the complete medical record. A million-token window is the entire medical record plus every relevant clinical guideline and research paper. But just as a physician with a thousand pages open on their desk does not actually process all of them simultaneously, a model with a massive context window does not attend equally to everything in it. The skill is in knowing which pages to have open.

## Why It Matters for Enterprise AI

Context window management is where many of the 42% of abandoned AI initiatives went wrong. They either stuffed too much irrelevant context (producing confused, expensive responses) or provided too little (producing ungrounded, hallucinated responses). Getting this right is operational, not theoretical.

Your institutional knowledge architecture directly determines context quality. Organizations that have structured their knowledge into retrievable, well-chunked, semantically organized documents can assemble precise, relevant context for every query. Organizations with knowledge trapped in sprawling SharePoint sites, undocumented processes, and tribal knowledge in people's heads cannot. The context window is finite and expensive. What you fill it with is the difference between a force multiplier and an expensive autocomplete. Your curated ground truth is what makes every token in that window count.

## Key Technical Details

- Token count: ~0.75 words per token (English); context measured in tokens not words
- Evolution: 4K (2022) → 32K → 128K → 200K → 1M+ tokens (2025-2026)
- Quadratic scaling: traditional attention cost scales as O(n^2) with context length
- Lost in the middle: models attend more to beginning and end of context
- Cost: proportional to input + output tokens; 100K context ~25x cost of 4K
- Efficient retrieval (RAG) outperforms brute-force context stuffing
- Sliding window / sparse attention: architectural innovations enabling longer contexts
- Practical sweet spot: most enterprise tasks need 4K-32K of well-curated context

## Related Terms

- [RAG](rag.md) - efficient context construction through targeted retrieval
- [Memory](memory.md) - persistence mechanisms beyond single context windows
- [Prompt Engineering](prompt-engineering.md) - the art of using context effectively
- [Inference](inference.md) - where context window constraints apply in real time

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
