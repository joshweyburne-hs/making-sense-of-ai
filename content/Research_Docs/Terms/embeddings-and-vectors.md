# Embeddings & Vectors

Embeddings are numerical representations of text that capture semantic meaning, converting words, sentences, and documents into arrays of numbers where similar meanings map to nearby positions in vector space. They are the index system that makes semantic search, and therefore RAG, possible.

## How It Works

Traditional text search is lexical: it matches keywords. Search for "heart attack" and you find documents containing those exact words. Miss "myocardial infarction," "cardiac event," and "MI" entirely. Embeddings solve this by converting text into high-dimensional vectors (typically 768 to 3,072 dimensions) where semantic similarity corresponds to geometric proximity.

An embedding model processes a piece of text and outputs a vector, a list of floating-point numbers. "Heart attack" and "myocardial infarction" produce vectors that are close together in this space because they appear in similar contexts in the training data. "Bicycle repair" produces a vector far away from both. The distance between vectors (typically measured by cosine similarity) quantifies semantic relatedness on a continuous scale.

The process for building a searchable knowledge base follows a clear pipeline. Documents are split into chunks of manageable size (256-1,024 tokens). Each chunk is run through an embedding model to produce a vector. These vectors are stored in a vector database alongside the original text. At query time, the user's question is embedded using the same model, and the database returns the chunks whose vectors are closest to the query vector. These retrieved chunks become the context for RAG.

Embedding models are specialized for this task. OpenAI's text-embedding-ada-002 and text-embedding-3-large, Cohere's embed models, and Snowflake's Arctic Embed family are purpose-built to produce high-quality semantic representations. They are smaller and faster than generation models because they only need to encode meaning, not produce text. The choice of embedding model directly affects retrieval quality: a poor embedding model that maps unrelated concepts to similar vectors will return irrelevant results regardless of how good the generation model is.

Vector databases are the storage and retrieval infrastructure. Pinecone, Weaviate, Chroma, Milvus, and Snowflake's native vector search provide optimized indexing for high-dimensional similarity search. They use approximate nearest neighbor algorithms (HNSW, IVF) to search billions of vectors in milliseconds, making real-time RAG retrieval feasible at enterprise scale.

## Medical Analogy

Embeddings are the conceptual index of a medical library, organized by meaning rather than alphabetically. An alphabetical index puts "angina" far from "chest pain" and "cardiac ischemia." A conceptual index places them together because they are semantically related. When a physician needs information about a patient's symptoms, they think in concepts, not keywords. Embeddings let machines do the same.

## Why It Matters for Enterprise AI

Embeddings are the infrastructure beneath RAG, and RAG is the mechanism that converts your institutional knowledge into AI capability. The quality of your embeddings directly determines the quality of your retrieval, which directly determines the quality of your AI outputs.

For the >80% of organizations seeing no meaningful EBIT impact from AI, the embedding layer is often where value silently leaks. Poor chunking strategies fragment important context across multiple chunks that are never retrieved together. Mismatched embedding models fail to capture domain-specific terminology. Stale indexes do not reflect current knowledge. These are not glamorous problems, but they are the ground truth of whether your RAG system actually works.

Your domain vocabulary is the strategic differentiator. A general-purpose embedding model may not distinguish between your product names, your internal acronyms, or your industry-specific terminology. Fine-tuning embedding models on your domain data, or selecting models trained on relevant corpora, ensures that your tribal knowledge is semantically indexed in ways that generic embeddings miss. This is codified craftsmanship at the infrastructure level: invisible to end users, but determinative of every answer the system produces.

## Key Technical Details

- Embedding dimensions: typically 768 to 3,072 floating-point numbers per vector
- Similarity metric: cosine similarity is standard; dot product and Euclidean distance also used
- Chunking strategy: 256-1,024 tokens per chunk with 10-20% overlap is common starting point
- Popular embedding models: OpenAI ada-002/3-large, Cohere embed, Snowflake Arctic Embed
- Vector databases: Pinecone, Weaviate, Chroma, Milvus, Snowflake native vector search
- Approximate nearest neighbor: HNSW and IVF algorithms enable millisecond search at scale
- Embedding model choice affects retrieval quality more than generation model choice
- Domain-specific fine-tuning of embeddings improves retrieval for specialized vocabularies

## Related Terms

- [RAG](rag.md) - the architecture that embeddings enable through semantic retrieval
- [Grounding](grounding.md) - the principle served by embedding-powered retrieval
- [Context Windows](context-windows.md) - where retrieved chunks are injected for generation
- [Memory](memory.md) - uses the same vector storage for persistent interaction recall

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
