# Grounding

Grounding is the practice of connecting LLM outputs to verifiable, authoritative sources rather than allowing the model to generate from its parametric memory alone. It transforms an unreliable oracle into a trustworthy assistant by anchoring every claim to evidence.

## How It Works

An ungrounded LLM generates responses based solely on patterns absorbed during training. It has no mechanism to distinguish what it "knows" from what it is fabricating. Grounding introduces external verification by providing the model with retrieved source material and instructing it to base its responses on that material rather than its internal weights.

Retrieval-Augmented Generation (RAG) is the primary grounding mechanism. When a user asks a question, the system first retrieves relevant documents from a knowledge base, injects them into the model's context window, and instructs the model to answer based on the provided sources. The model generates a response that references specific passages, effectively converting from "I think the answer is..." to "According to [source], the answer is..."

Citation and attribution are the visible markers of grounding. A well-grounded system does not just produce correct answers; it tells you exactly where each claim came from. This enables verification: a human reviewer can check the cited source and confirm the model's interpretation. Some systems produce grounding scores, numerical confidence measures indicating how strongly the response is supported by retrieved evidence.

Knowledge cutoff awareness is another dimension of grounding. Every model has a training data cutoff date beyond which it has no information. Grounded systems acknowledge these boundaries rather than confabulating. When the model cannot find relevant retrieved information to answer a question, a properly grounded system says "I don't have information about that" rather than inventing a plausible response.

Tool use extends grounding beyond static documents. A grounded system can call APIs for current stock prices, query databases for real-time inventory, or search the web for recent events. Each tool call provides fresh, verifiable data that anchors the model's response to current reality rather than stale training data.

## Medical Analogy

Grounding is evidence-based medicine. Before the evidence-based movement, physicians relied on experience, intuition, and tradition. Evidence-based medicine demands that clinical decisions be grounded in peer-reviewed research, clinical trials, and systematic reviews. A physician who says "In my experience, this treatment works" is ungrounded. One who says "The NEJM meta-analysis of 12 randomized trials shows a 34% reduction in mortality" is grounded. Both might reach the same conclusion, but only the second can be verified and trusted.

## Why It Matters for Enterprise AI

Grounding is the bridge between AI capability and enterprise trust. The reason <25% of AI initiatives move from pilot to production is not that models are not capable enough; it is that organizations cannot trust ungrounded outputs at scale. When a model confidently generates a response about your product specifications, your compliance requirements, or your customer history, you need to know whether that response comes from your actual documentation or from the model's imagination.

Your institutional knowledge is the grounding material. Every product spec, process document, compliance framework, and verified procedure in your organization is a potential grounding source. This is where the strategic moat forms: your competitors can buy the same model, but they cannot ground it in your proprietary knowledge base. The more complete and well-curated your ground truth, the more reliable your AI outputs become. Grounding scores above 0.9 are achievable when retrieval surfaces high-quality, relevant institutional documentation. Below 0.7, the system is essentially confabulating with a veneer of confidence. Your investment in knowledge management directly determines where you land on that spectrum.

## Key Technical Details

- RAG is the primary grounding mechanism: retrieve then generate
- Grounding scores: numerical confidence (0-1) measuring source support for claims
- Citation attribution: linking specific claims to specific source passages
- Knowledge cutoff: every model has a training data boundary it cannot see past
- Tool use: APIs, databases, and web search provide real-time grounding
- Ungrounded hallucination: 9.2-15.6%; grounded hallucination: <0.9%
- Source quality determines output quality: garbage in, grounded garbage out
- Multi-source grounding: cross-referencing multiple documents increases reliability

## Related Terms

- [RAG](rag.md) - the primary mechanism for implementing grounding
- [Hallucination](hallucination.md) - the failure mode grounding prevents
- [Embeddings & Vectors](embeddings-and-vectors.md) - the retrieval technology powering grounded search
- [Context Windows](context-windows.md) - the space where grounding material is injected

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
