# Tokenization

Tokenization is the process of breaking raw text into discrete units called tokens that a language model can process numerically. It is the first and last step in every LLM interaction: text is tokenized into numbers on input, and numbers are decoded back into text on output.

## How It Works

LLMs do not read characters or words directly. They operate on tokens, which are subword units derived from statistical analysis of training text. The three dominant tokenization approaches are Byte Pair Encoding (BPE), WordPiece, and SentencePiece.

BPE, used by GPT models and Llama, starts with individual characters and iteratively merges the most frequently co-occurring pairs until reaching a target vocabulary size. The word "understanding" might become ["under", "stand", "ing"]. Common words like "the" get their own token. Rare words get split into subword pieces. This balances vocabulary size against the ability to represent any text, including misspellings and neologisms.

WordPiece, used by BERT and some Google models, works similarly but selects merges based on likelihood improvement rather than raw frequency. SentencePiece treats the input as a raw byte stream, making it language-agnostic and eliminating the need for pre-tokenization rules. This is critical for multilingual models.

Modern tokenizers have vocabularies of roughly 50,000 to 100,000 tokens. For English text, the average ratio is approximately 1.3 tokens per word, though this varies significantly. Code and technical text tend to be more token-dense. Non-English languages, particularly those with non-Latin scripts, often require more tokens per equivalent meaning, creating a fairness and cost disparity.

Tokenization directly affects two critical operational metrics: cost and context windows. API providers charge per token (input and output). Context windows are measured in tokens, not words. A 128K token context window holds roughly 98,000 English words, but significantly less in languages like Japanese or Arabic. Understanding tokenization is essential for estimating costs and designing prompts that fit within limits.

## Medical Analogy

Tokenization is like medical terminology. Physicians do not process language word by word like a layperson. They use specialized vocabulary where single terms ("tachycardia," "hypertension") compress complex concepts into efficient units. Similarly, a tokenizer compresses common patterns into single tokens while breaking unfamiliar terms into recognizable subparts. The efficiency of communication depends on how well the vocabulary matches the content.

## Why It Matters for Enterprise AI

Tokenization seems like a low-level implementation detail, but it has direct financial and operational consequences. Every API call to a frontier model is billed per token. If your enterprise processes millions of documents, tokenization efficiency directly affects your AI operating costs. More importantly, context window limits are token limits. When you are feeding your institutional knowledge into a model, whether through RAG or long-context prompting, you are constrained by how efficiently your content tokenizes. Domain-specific jargon, product codes, and internal terminology may tokenize poorly with general-purpose tokenizers, consuming more of your context budget than expected. Understanding this helps you design systems that use your context window budget wisely, ensuring the model sees the ground truth it needs to deliver value instead of burning tokens on inefficient encoding. The 42% of abandoned AI initiatives often stumble on practical issues exactly like this.

## Key Technical Details

- BPE (Byte Pair Encoding): used by GPT-4, Llama, most open models
- WordPiece: used by BERT-family models
- SentencePiece: language-agnostic, treats input as raw bytes
- Typical vocabulary size: 50K-100K tokens
- Average English ratio: ~1.3 tokens per word
- Tokenization is deterministic: same input always produces same tokens
- Special tokens: [BOS] (beginning of sequence), [EOS] (end), [PAD], [SEP]
- Non-English languages often require 2-4x more tokens per equivalent meaning
- Tiktoken (OpenAI) and Hugging Face Tokenizers are the standard libraries

## Related Terms

- [LLM Architecture](llm-architecture.md)
- [Pre-training](pre-training.md)
- [Weights & Parameters](weights-and-parameters.md)
- [Training Data](training-data.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
