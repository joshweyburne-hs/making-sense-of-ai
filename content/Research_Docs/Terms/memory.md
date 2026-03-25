# Memory

Memory is the ability of an LLM system to retain and use information across interactions, transforming isolated one-off exchanges into persistent, evolving relationships. Without memory, every conversation starts from zero.

## How It Works

LLMs themselves have no built-in memory between sessions. Each inference call processes a context window in isolation. Memory is an architectural feature built around the model, not within it, and it comes in two fundamental forms.

In-context memory is short-term retention within a single conversation. As you chat with a model, the entire conversation history is fed back into the context window with each new message. The model "remembers" what you said earlier because it can see the full transcript. This works well for conversations that fit within the context window, but degrades as conversations grow long: older messages get truncated or summarized to make room for new ones. The lost-in-the-middle problem compounds here, with early conversation turns losing influence as the context fills.

Persistent memory operates across sessions, storing information externally and retrieving it when relevant. This takes several forms. Conversation summaries compress prior interactions into compact representations. User profiles accumulate preferences, roles, and past decisions. External memory stores, vector databases or structured knowledge bases, hold retrieved facts and prior interactions indexed for semantic retrieval. When a new conversation begins, the system queries these stores and injects relevant history into the context.

The curation challenge is the hard problem of memory. A system that remembers everything drowns in noise. A system that remembers nothing wastes every prior interaction. Effective memory systems must decide what to store (significant decisions, stated preferences, factual corrections), what to discard (casual remarks, one-time requests), and what to update (preferences that change, information that becomes stale). This is an active area of research with no solved solutions, most current systems err on the side of remembering too much.

Architecturally, memory systems typically combine a short-term buffer (recent conversation), a working memory (currently active context), and a long-term store (persistent facts and history). Retrieval from long-term memory uses the same embedding and vector search techniques that power RAG, making memory and retrieval architecturally similar systems serving different purposes.

## Medical Analogy

Memory is the electronic health record. A physician without access to patient history treats every visit as a first encounter. A physician with comprehensive records knows your allergies, your medication history, your chronic conditions, and the reasoning behind past treatment decisions. The difference is not just convenience; it is safety. Memory prevents repeating failed approaches, ensures continuity of care, and enables treatment plans that build on prior progress.

## Why It Matters for Enterprise AI

Memory is what turns an AI chatbot into an AI colleague. The difference between a system that asks "What do you do?" every session and one that says "Last time we discussed the Q3 pipeline risk in your Northeast territory" is the difference between a demo and a tool people actually use.

For the >80% of organizations seeing no meaningful EBIT impact from AI, memory is often the missing ingredient. Their AI systems cannot accumulate institutional knowledge over time. Every interaction is stateless, every answer decontextualized. Building memory systems that capture your organizational ground truth, decision patterns, and relationship context means AI that compounds in value with use rather than resetting to zero with each session. This is the long game of enterprise AI: not a one-time deployment, but a system that gets better as it accumulates your codified craftsmanship. The organizations that solve memory will have AI systems that understand their business deeply, and that understanding becomes a strategic moat competitors cannot replicate overnight.

## Key Technical Details

- In-context memory: conversation history within a single context window
- Persistent memory: external stores queried across sessions
- Memory types: conversation summaries, user profiles, factual stores, interaction logs
- Curation problem: what to remember, forget, and update is unsolved
- Vector-based retrieval: same embeddings technology as RAG, different purpose
- Memory architecture: short-term buffer + working memory + long-term store
- Context window limits force memory compression and summarization
- Privacy and security: persistent memory creates data retention and access control requirements

## Related Terms

- [Context Windows](context-windows.md) - the working memory constraint for each interaction
- [RAG](rag.md) - architecturally similar retrieval system for knowledge rather than memory
- [Embeddings & Vectors](embeddings-and-vectors.md) - the indexing technology enabling memory retrieval
- [Agents](agents.md) - the primary consumers of persistent memory across tasks

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
