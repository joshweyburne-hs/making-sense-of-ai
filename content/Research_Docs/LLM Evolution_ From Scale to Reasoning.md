# **The Post-Training Paradigm: From Scale-First Architectures to the Era of Deliberate Analytical Processing and Human-Centric Alignment**

The trajectory of large language models has undergone a fundamental transformation, moving away from a singular focus on parameter expansion toward a more nuanced mastery of analytical deliberation, logic, and human-aligned values. While the initial era of deep learning for natural language processing was defined by the transition from rigid, rule-based systems to flexible neural architectures, the modern frontier is characterized by the optimization of inference-time compute and the curation of high-fidelity human expertise. This evolution reflects a broader realization within the field: that raw scale, while necessary, is insufficient for achieving the level of reliability and sophisticated multi-step problem-solving required for autonomous agents and expert-level domains.

## **The Genesis of Modern Language Modeling and the Neural Transition**

The history of language modeling begins with the rigid, symbolic systems of the mid-20th century. Early implementations like ELIZA (1966) relied on pattern matching and hardcoded grammars to simulate structured dialogue, but these systems lacked genuine comprehension and the ability to generalize across domains.1 The 1990s marked a significant shift toward statistical methods, where language generation was modeled probabilistically. Techniques such as n-gram models, hidden Markov models (HMMs), and conditional random fields (CRFs) enabled more data-driven approaches, particularly in machine translation and speech recognition.2 However, these statistical models were inherently constrained by limited context windows and an inability to capture deeper semantic dependencies.2

The first major neural revolution occurred in the early 2010s with the development of word embeddings and the application of recurrent neural networks (RNNs) and long short-term memory (LSTM) networks.2 In 2013, the introduction of Word2Vec captured word meanings by placing them in a multi-dimensional space, allowing machines to represent semantic similarity mathematically.1 Subsequent sequence-to-sequence (seq2seq) models using LSTMs improved the ability to handle sequential data, and by 2016, major services like Google Translate had transitioned from statistical phrase-based models to deep recurrent neural networks.3 Despite these breakthroughs, early neural models suffered from several critical limitations: they processed inputs sequentially, were difficult to parallelize, and struggled with long-term dependencies due to vanishing or exploding gradients.2

### **The Transformer and the Catalyst of Self-Attention**

The introduction of the Transformer architecture in the 2017 paper "Attention Is All You Need" represented a definitive break from the sequential paradigm.5 By dispensing with recurrence and convolutions entirely, the Transformer relied on a fully parallel attention mechanism known as self-attention.4 This architectural shift was the catalyst for the "scale-first" era, as it enabled massive parallelization on GPU hardware, allowing models to be trained on unprecedented volumes of data.4

The core of this innovation is the self-attention mechanism, which relates different positions of a single sequence to compute a representation of that sequence.6 Mathematically, each word or token computes relevance scores with every other token in the context window. This process involves three learned linear projections: Query (![][image1]), Key (![][image2]), and Value (![][image3]). The attention score is derived as a weighted combination of these values:

![][image4]  
where ![][image5] is the dimension of the key vectors.5 This formulation allows the model to resolve ambiguities by assigning higher weights to relevant contextual markers, regardless of their distance in the sequence.4 Multi-head attention further enhances this by introducing multiple parallel attention heads, each learning different linear projections of the ![][image1], ![][image2], and ![][image3] matrices, thereby capturing varied aspects of word relationships simultaneously.5

| Architectural Feature | RNN / LSTM | Transformer |
| :---- | :---- | :---- |
| **Computation Style** | Sequential (step-by-step) | Parallel (entire sequence) |
| **Path Length** | **![][image6]** (gradient flow length) | ![][image7] (global access) |
| **Hardware Utilization** | Limited (low GPU parallelization) | High (optimized for matrix math) |
| **Contextual Memory** | Hidden state (information bottleneck) | Self-attention (all-to-all access) |
| **Scaling Potential** | Low (computational bottlenecks) | Extremely High (parameters and data) |

2

## **The Pre-training Era and the Evolution of Data Composition**

As the Transformer architecture provided the necessary scalability, the focus of the field shifted to the composition and scale of pre-training data. Initially, models like the original GPT were trained on single domains, but the release of GPT-2 and GPT-3 popularized the use of massive, general-purpose web scrapes.9 Common Crawl, a vast archive of the public internet spanning over 17 years, became the foundational corpus for modern large-scale training.9

The evolution of pre-training datasets progressed from raw web crawls to meticulously cleaned and deduplicated corpora. The Colossal Clean Crawled Corpus (C4), created in 2019, was one of the first datasets to apply extensive preprocessing to remove "gibberish" and non-textual elements, setting a new standard for data quality.10 This trajectory continued with datasets like MassiveText, which exceeded 2 trillion tokens by incorporating diverse sources like books, news, and scientific articles, and RefinedWeb, which emphasized that high-quality web data alone, if rigorously filtered, could outperform mixed-source datasets.10

### **The Data Wall and the Pivot to Textbook-Grade Quality**

By 2024, the field encountered a "Data Wall"—the point where simply adding more raw data from the web yielded diminishing returns.10 This realization was compounded by the fact that less than 5% of remaining web-scale content met the quality and licensing standards suitable for frontier training.12 In response, researchers pivoted toward "textbook-grade" data, which prioritizes logical structure, clear explanations, and educational value.10

The Phi series of models demonstrated the power of this approach. Phi-1 (1.3 billion parameters) was trained using a selection of "textbook quality" data from the web (6B tokens) and synthetically generated textbooks created with GPT-3.5 (1B tokens), allowing it to match the performance of models 25 times its size on coding tasks.13 The methodology involved using a frontier model as a classifier to determine the "educational value" of web content, focusing on topics that promote analytical skill and basic algorithmic logic.14

| Pre-training Dataset | Volume (Approx.) | Primary Methodology | Key Model |
| :---- | :---- | :---- | :---- |
| **C4 (2019)** | 156B tokens | Raw Common Crawl filtering | T5 |
| **GPT-3 (2020)** | 300B tokens | Filtered web \+ books \+ Wikipedia | GPT-3 |
| **RedPajama (2023)** | 1.2T tokens | Open-source Llama reproduction | Llama-like |
| **RefinedWeb (2023)** | 5T tokens | Aggressive deduplication/cleaning | Falcon |
| **FineWeb (2024)** | 15T tokens | Trafilatura extraction \+ MinHash | Llama-3 class |
| **FineWeb-Edu (2025)** | 1.3T tokens | Classifier-based educational filtering | Compact reasoning models |

10

### **Empirical Scaling Laws: From Kaplan to Chinchilla**

Understanding the optimal allocation of computational resources became a central pursuit during the pre-training era. Initial research by Kaplan et al. (2020) suggested that model size should be increased more quickly than data as the compute budget grows, leading to the development of massive models like GPT-3 with relatively sparse training data.17 However, the "Chinchilla" scaling laws, introduced by Hoffmann et al. in 2022, revised this finding.17

Chinchilla scaling dictates that for a given compute budget (![][image8]), parameters (![][image9]) and training tokens (![][image10]) should be scaled in equal proportions: ![][image11] and ![][image12].17 The parametric loss function used to model this relationship is:

![][image13]  
where ![][image14] represents the irreducible loss of an ideal generative process, and ![][image15] are empirically fitted coefficients.19 This insight revealed that many frontier models were "under-trained," prompting a shift toward training smaller, more efficient models on trillions of additional tokens (e.g., Llama 3\) to optimize for both training efficiency and inference-time costs.17

## **Post-Training and the Alignment Revolution**

While pre-training imparts general world knowledge and linguistic patterns, the resulting base models are often unaligned with specific user intentions or safety guidelines. Post-training has evolved from simple task-specific fine-tuning to a sophisticated multi-stage alignment process involving supervised and reinforcement learning.2

### **Supervised Fine-Tuning (SFT) and Instruction Following**

Supervised Fine-Tuning (SFT) serves as the initial phase of alignment, where the model is trained on a curated dataset of instruction-response pairs.22 This stage teaches the model general instruction-following behavior and establishes a "starting policy" for subsequent alignment steps.23 SFT is highly effective for tasks with clear, correct answers, such as formatting responses in JSON or adopting a specific professional tone.24 However, SFT acts as an "imitator"; it lacks the mechanism to internalize the relative ranking between different response options and can suffer from "catastrophic forgetting" if pushed too far on a narrow dataset.22

### **Reinforcement Learning from Human Feedback (RLHF) and PPO**

To refine model behavior beyond simple imitation, researchers employ Reinforcement Learning from Human Feedback (RLHF). This pipeline typically involves training a separate "reward model" based on human preferences (ranking multiple outputs for a single prompt) and then using that model to guide the language model's policy via Proximal Policy Optimization (PPO).22

PPO is widely utilized because it ensures stable and controlled learning by limiting how much the model's behavior can shift in a single update.27 It uses a "clipped surrogate loss" to prevent drastic changes that could destabilize the training of large-scale models.25 While powerful, RLHF with PPO is computationally intensive, requiring the simultaneous maintenance of multiple models (policy, reference, reward, and value models) and sensitive hyperparameter tuning.22

### **Direct Preference Optimization (DPO): The Offline Alternative**

In 2024 and 2025, Direct Preference Optimization (DPO) emerged as a significant alternative to the RLHF/PPO paradigm. DPO eliminates the need for a separate reward model and an online RL loop by treating preference data as implicit supervision.22 It directly adjusts model parameters to increase the probability of preferred responses over rejected ones using a binary cross-entropy loss function.23

Empirical comparisons indicate that while DPO is more stable and computationally efficient for conversational tasks and summarization, PPO still tends to outperform DPO in structured, complex domains like mathematical deliberation and code generation.25 This suggests that the "exploration" phase inherent in online reinforcement learning is critical for discovering optimal strategies in complex multi-step problems.25

| Alignment Technique | Primary Data Requirement | Technical Mechanism | Core Strength |
| :---- | :---- | :---- | :---- |
| **SFT** | Instruction-answer pairs | Negative log-likelihood loss | Style, format, and imitation |
| **RLHF (PPO)** | Human-ranked preferences | Clipped surrogate loss \+ RM | Nuanced reasoning and safety |
| **DPO** | Pairwise (chosen/rejected) | Direct log-likelihood ratio | Stability and compute efficiency |
| **ORPO** | Pairwise (chosen/rejected) | Odds ratio penalty in NLL | Integrated one-stage alignment |
| **GRPO** | Group-based rewards | Advantage estimation (no critic) | Efficient reasoning scaling |

22

## **The Reasoning Revolution: Systems 1 and 2 and Inference-Time Scaling**

The most transformative shift in current model development (2024–2026) is the transition from "System 1" thinking—fast, automatic token prediction—to "System 2" thinking—deliberate, slow, and conscious analytical processing.32 This paradigm, popularized by models such as OpenAI o1 and DeepSeek R1, allows models to "think" for longer periods before generating a final response, significantly improving performance on complex, logical tasks.34

### **Native Step-by-Step Deliberation and Inference Compute**

Traditional language models use "train-time compute scaling," where model capability is primarily determined by pre-training resources.37 The new generation of Large Reasoning Models (LRMs) introduces "test-time compute scaling," dynamically allocating more computational resources at the point of inference.34 For instance, OpenAI o1 was trained via a data-efficient reinforcement learning algorithm that teaches the model how to use an internal chain of thought to break down complex problems, recognize errors, and refine strategies.34

This shift has profound implications for scaling laws. While the gains from pre-training begin to plateau as public data runs dry, model performance on benchmarks like AIME (math) or GPQA (science) continues to improve as more "thinking time" (test-time compute) is allocated to the query.34 This process allows a 7B parameter model with extended deliberation to match the performance of a 70B parameter model using standard autoregressive generation.36

### **Process Supervision vs. Outcome Supervision**

To effectively train models in multi-step deliberation, the field has moved away from "Outcome-supervised Reward Models" (ORMs)—which only provide a reward for the final answer—toward "Process-supervised Reward Models" (PRMs).39 PRMs provide feedback and credit assignment for each intermediate reasoning step, which is essential for complex tasks where a model might reach the correct answer through flawed logic.40

OpenAI's research demonstrated that PRMs significantly outperform ORMs on the challenging MATH dataset, achieving 78.2% accuracy by verifying every step of the solution.39 This stepwise verification also facilitates advanced search techniques at inference time, such as Monte Carlo Tree Search (MCTS) or "Best-of-N" sampling, where the model can prune incorrect reasoning paths early and focus its compute on branches with higher likelihoods of success.38

| Feature | Outcome Supervision (ORM) | Process Supervision (PRM) |
| :---- | :---- | :---- |
| **Feedback Timing** | Only at the end of output | After every logical step |
| **Signal Density** | Sparse (Binary success/fail) | Dense (Fine-grained scores) |
| **Interpretability** | Opaque logic | Transparent reasoning chain |
| **Alignment Risk** | High (reward hacking) | Low (verification of logic) |
| **Inference Usage** | Post-generation re-ranking | Step-by-step guided decoding |

39

## **The Human Data Shift: Expert Feedback as the Primary Bottleneck**

As internet-scale data becomes insufficient for frontier capabilities, the focus of the training pipeline has shifted toward the "Human-in-the-loop" (HITL).44 The bottleneck for the next generation of models is no longer just raw text, but high-quality, human-curated reasoning traces.11

### **The Expert Economy and Credentialed Annotation**

Earlier stages of AI development relied on low-wage contractors to perform simple data labeling tasks.11 In contrast, current frontier labs are racing to secure credentialed professionals—PhDs, physicians, lawyers, and expert software developers—to design evaluation rubrics and score complex reasoning chains.11 Companies like Scale AI, Labelbox, and Invisible now hire these experts at rates between $50 and $250 per hour to generate the preference data that shapes the behavior of the most advanced models.11

This shift represents a fundamental change in the economics of AI: the primary marginal cost of training a frontier model is now the acquisition of high-quality human expertise, which is outpacing the cost of raw compute.47 This human data is essential for capturing unique, practical knowledge (e.g., financial forecasting or clinical diagnostics) that is rarely documented in detail on the public web.46

### **Synthetic Data and the Risk of Model Collapse**

While synthetic data (data generated by other models) is used to scale training pipelines, it remains a "qualified yes" in terms of its benefits.46 Synthetic data can help re-balance datasets or simulate rare "edge cases," but without rigorous human oversight, it can lead to "model collapse"—a state where models trained on AI-generated content begin to lose their ability to generate diverse, high-quality outputs and overfit on their own artifacts.49 Strategic sampling and human-in-the-loop validation are therefore critical for preventing drift and ensuring that synthetic datasets maintain grounding in real-world logic.50

## **Evaluation and Safety: Beyond Saturated Benchmarks**

The maturity of Large Language Models has rendered traditional academic benchmarks like MMLU increasingly irrelevant for distinguishing between frontier models. By early 2026, leading models had saturated the original MMLU, making its scores less informative for production outcomes.53

### **The Shift to Private and reasoning-Focused Evaluation**

In response to saturation and data contamination (where test questions appear in the training set), frontier labs have moved toward custom, private evaluation sets and more difficult benchmarks:

* **MMLU-Pro**: Replaces trivial factual questions with reasoning-focused problems and expands multiple-choice options from 4 to 10 to reduce the impact of random guessing.53  
* **GPQA Diamond**: PhD-level science questions in physics, biology, and chemistry that are designed to be difficult even for experts in the field to answer without significant effort.34  
* **AIME 2025/2026**: High-level mathematics competition problems used as the gold standard for evaluating multi-step analytical deliberation.36  
* **SWE-bench Verified**: Real-world software engineering tasks that require models to resolve actual GitHub issues, providing a more practical measure of agentic capability.37

### **Technical Implementation of Guardrails**

Safety mechanisms, known as guardrails, have evolved from simple keyword filters into sophisticated, model-assisted layers that monitor both input handling and output generation.56 These systems defend against prompt injection, jailbreaking, and hallucinations by validating the model's responses against a rubric of safety policies.56

A critical challenge is integrating these guardrails without "lobotomizing" model intelligence—a phenomenon where overly restrictive filters cause the model to over-refuse benign requests or lose creative flexibility.58 Modern implementations use "layered guardrails," combining lightweight pre-processing input checks with more intensive post-processing output validation.57 Adversarial training using automated "fuzzers" like AdvJudge-Zero identifies logic flaws in these guardrails, allowing developers to retrain models to be more robust against stealthy input sequences without sacrificing performance on complex tasks.61

| Security Mechanism | Lifecycle Phase | Primary Goal | Detection Strategy |
| :---- | :---- | :---- | :---- |
| **Input Guardrail** | Pre-processing | Stop malicious prompts | ML classification / intent analysis |
| **Syntax Guardrail** | Generation | Ensure valid data formats | Schema validation (JSON/XML) |
| **DLP Guardrail** | Post-processing | Prevent data leakage | PII scanning / secret detection |
| **Output Guardrail** | Post-processing | Filter harmful content | Safety classifiers / LLM-as-a-judge |
| **Adversarial Training** | Post-training | Harden core behavior | Red-teaming / automated fuzzing |

56

## **Current Frontier Bottlenecks**

As of 2026, the primary obstacles for frontier labs have shifted from architectural innovation to systemic and logistical constraints:

1. **Expert Data Scarcity**: The global supply of credentialed human intelligence is limited. Recruiting PhDs and licensed professionals to label reasoning traces has become more expensive than the marginal compute required for training.11  
2. **Inference Latency in LRMs**: While test-time compute scaling dramatically improves accuracy, it increases latency and cost per query.34 Techniques like parallel reasoning (ThreadWeaver) are being developed to mitigate this by concurrent exploration of reasoning paths.36  
3. **Benchmark Saturation and Contamination**: Public benchmarks are no longer reliable predictors of production performance. Labs must build proprietary, rotating test sets and use human spot evaluations to verify real-world utility.54  
4. **Inference Compute Infrastructure**: The demand for inference-optimized architecture (e.g., NVIDIA Blackwell, TPU v5e) is projected to exceed training demand by over 100x by late 2026, as models consume significantly more tokens during their internal deliberation phases.36  
5. **Alignment-Intelligence Trade-offs**: Ensuring safety without reducing the model's creative and analytical capacity remains a delicate balancing act, requiring more nuanced, graded evaluation rather than binary "block/allow" logic.58

### **The Human-in-the-Loop as the Final Frontier**

The most valuable part of the training pipeline is now the expert human who provides the "ground truth" for complex reasoning. Large Language Models have moved from being repositories of internet data to being reasoning engines that learn from the collective judgment of experts.12

The "Human-in-the-loop" is no longer just about cleaning data; it is about acting as the architect of decision logic.48 Whether it is evaluating whether a software agent took safe, interpretable steps in a deployment environment or ensuring that a model's internal reasoning adheres to ethical transparency, human expertise remains the irreplaceable anchor for frontier AI.44 As synthetic data reaches its limits and the web's reservoir runs dry, the next wave of breakthroughs will come from the data engines that encode human judgment, structure, and skill into continuous learning loops.12 This transition marks the end of the "scale-first" era and the beginning of a new paradigm where intelligence is defined by the quality of the deliberation and its alignment with human-centric expertise.

#### **Works cited**

1. Evolution of Large Language Models (2026 Updated) \- The Expert Community, accessed March 22, 2026, [https://theexpertcommunity.com/artificial-intelligence/evolution-of-large-language-models/](https://theexpertcommunity.com/artificial-intelligence/evolution-of-large-language-models/)  
2. A Survey of Large Language Models: Evolution, Architectures, Adaptation, Benchmarking, Applications, Challenges, and Societal Implications \- MDPI, accessed March 22, 2026, [https://www.mdpi.com/2079-9292/14/18/3580](https://www.mdpi.com/2079-9292/14/18/3580)  
3. Large language model \- Wikipedia, accessed March 22, 2026, [https://en.wikipedia.org/wiki/Large\_language\_model](https://en.wikipedia.org/wiki/Large_language_model)  
4. Self-Attention Explained Clearly: The Core Mechanism Behind LLM Intelligence \- Medium, accessed March 22, 2026, [https://medium.com/@dhruvsharmaaugust2003/self-attention-explained-clearly-the-core-mechanism-behind-llm-intelligence-50e04263e4ba](https://medium.com/@dhruvsharmaaugust2003/self-attention-explained-clearly-the-core-mechanism-behind-llm-intelligence-50e04263e4ba)  
5. Attention Is All You Need \- Wikipedia, accessed March 22, 2026, [https://en.wikipedia.org/wiki/Attention\_Is\_All\_You\_Need](https://en.wikipedia.org/wiki/Attention_Is_All_You_Need)  
6. Attention Is All You Need \- arXiv, accessed March 22, 2026, [https://arxiv.org/html/1706.03762v7](https://arxiv.org/html/1706.03762v7)  
7. I Finally Understood “Attention is All You Need” After So Long. Here's How I Did It., accessed March 22, 2026, [https://ai.plainenglish.io/i-finally-understood-attention-is-all-you-need-after-so-long-heres-how-i-did-it-263b46273f9f](https://ai.plainenglish.io/i-finally-understood-attention-is-all-you-need-after-so-long-heres-how-i-did-it-263b46273f9f)  
8. Self-Attention: The Simple Mechanism That Made ChatGPT Possible | by Debasish Das, accessed March 22, 2026, [https://pub.towardsai.net/transformer-architecture-self-attention-3f947540871d](https://pub.towardsai.net/transformer-architecture-self-attention-3f947540871d)  
9. Building an LLM Stack Part 2: Pre-training Tips & Data Processing Tricks \- Deepgram, accessed March 22, 2026, [https://deepgram.com/learn/building-an-llm-stack-part-2-pre-training-tips-data-processing-tricks](https://deepgram.com/learn/building-an-llm-stack-part-2-pre-training-tips-data-processing-tricks)  
10. How Have Pre-Training Datasets for Large Language Models ..., accessed March 22, 2026, [https://medium.com/@jelkhoury880/how-have-pre-training-datasets-for-large-language-models-evolved-13d74c01f8e8](https://medium.com/@jelkhoury880/how-have-pre-training-datasets-for-large-language-models-evolved-13d74c01f8e8)  
11. Beyond GPUs: Why Frontier Labs Are Now Racing to Secure Human Expertise \- VKTR, accessed March 22, 2026, [https://www.vktr.com/ai-market/beyond-gpus-why-frontier-labs-are-now-racing-to-secure-human-expertise/](https://www.vktr.com/ai-market/beyond-gpus-why-frontier-labs-are-now-racing-to-secure-human-expertise/)  
12. Why expert data is becoming the new fuel for AI models \- SignalFire, accessed March 22, 2026, [https://www.signalfire.com/blog/expert-data-is-new-fuel-for-ai-models](https://www.signalfire.com/blog/expert-data-is-new-fuel-for-ai-models)  
13. Phi-3 Technical Report: A Highly Capable Language Model Locally on Your Phone, accessed March 22, 2026, [https://arxiv.org/html/2404.14219v1](https://arxiv.org/html/2404.14219v1)  
14. Papers Explained 114: Phi-1 \- Ritvik Rastogi \- Medium, accessed March 22, 2026, [https://ritvik19.medium.com/papers-explained-114-phi-1-14a8dcc77ce5](https://ritvik19.medium.com/papers-explained-114-phi-1-14a8dcc77ce5)  
15. Textbooks Are All You Need II: phi-1.5 technical report \- Microsoft Research, accessed March 22, 2026, [https://www.microsoft.com/en-us/research/publication/textbooks-are-all-you-need-ii-phi-1-5-technical-report/](https://www.microsoft.com/en-us/research/publication/textbooks-are-all-you-need-ii-phi-1-5-technical-report/)  
16. Data for LLM pretraining \- LiU NLP, accessed March 22, 2026, [https://liu-nlp.ai/ete387-autumn/units/unit3/NLP-2025-33.pdf](https://liu-nlp.ai/ete387-autumn/units/unit3/NLP-2025-33.pdf)  
17. Neural scaling law \- Wikipedia, accessed March 22, 2026, [https://en.wikipedia.org/wiki/Neural\_scaling\_law](https://en.wikipedia.org/wiki/Neural_scaling_law)  
18. Scaling Laws for Neural Language Models \- arXiv, accessed March 22, 2026, [https://arxiv.org/pdf/2001.08361](https://arxiv.org/pdf/2001.08361)  
19. Chinchilla Scaling Law Overview \- Emergent Mind, accessed March 22, 2026, [https://www.emergentmind.com/topics/chinchilla-scaling-law](https://www.emergentmind.com/topics/chinchilla-scaling-law)  
20. Scaling Laws for LLM Pretraining \- Jonas Vetterle Personal Page & Blog, accessed March 22, 2026, [https://www.jonvet.com/blog/llm-scaling-laws](https://www.jonvet.com/blog/llm-scaling-laws)  
21. Chinchilla data-optimal scaling laws: In plain English \- LifeArchitect.ai, accessed March 22, 2026, [https://lifearchitect.ai/chinchilla/](https://lifearchitect.ai/chinchilla/)  
22. Improving LLM Safety and Helpfulness using SFT and DPO: A Study on OPT-350M \- arXiv, accessed March 22, 2026, [https://arxiv.org/html/2509.09055v1](https://arxiv.org/html/2509.09055v1)  
23. Fine-Tuning Techniques \- Choosing Between SFT, DPO, and RFT (With a Guide to DPO), accessed March 22, 2026, [https://developers.openai.com/cookbook/examples/fine\_tuning\_direct\_preference\_optimization\_guide](https://developers.openai.com/cookbook/examples/fine_tuning_direct_preference_optimization_guide)  
24. SFT vs. DPO: Comparison between LLM Alignment techniques | by Sulbha Jain | Medium, accessed March 22, 2026, [https://sulbhajain.medium.com/sft-vs-dpo-comparison-between-llm-alignment-techniques-26b6d76171da](https://sulbhajain.medium.com/sft-vs-dpo-comparison-between-llm-alignment-techniques-26b6d76171da)  
25. DPO vs PPO for LLMs: Key Differences & Use Cases \- Clarifai, accessed March 22, 2026, [https://www.clarifai.com/blog/dpo-vs-ppo](https://www.clarifai.com/blog/dpo-vs-ppo)  
26. SFT vs. DPO (/ RLHF)- A Visual Guide to What Your LLM Actually Learns | Sifal Klioui, accessed March 22, 2026, [https://sifal.social/posts/SFT-vs-DPO-A-Visual-Guide-to-LLM-Fine-Tuning/](https://sifal.social/posts/SFT-vs-DPO-A-Visual-Guide-to-LLM-Fine-Tuning/)  
27. RLHF, PPO, and DPO: How AI Models Learn from Human Preferences | Manchester Digital, accessed March 22, 2026, [https://www.manchesterdigital.com/post/ve3/rlhf-ppo-and-dpo-how-ai-models-learn-from-human-preferences](https://www.manchesterdigital.com/post/ve3/rlhf-ppo-and-dpo-how-ai-models-learn-from-human-preferences)  
28. DeepSeek R1, A New Chapter in Inference-Time Scaling for Reasoning Models \- Medium, accessed March 22, 2026, [https://medium.com/@saehwanpark/deepseek-r1-a-new-chapter-in-inference-time-scaling-for-reasoning-models-reviewing-deepseek-bae149ca88bc](https://medium.com/@saehwanpark/deepseek-r1-a-new-chapter-in-inference-time-scaling-for-reasoning-models-reviewing-deepseek-bae149ca88bc)  
29. ICML Poster DPO Meets PPO: Reinforced Token Optimization for RLHF, accessed March 22, 2026, [https://icml.cc/virtual/2025/poster/45726](https://icml.cc/virtual/2025/poster/45726)  
30. Unpacking DPO and PPO: Disentangling Best Practices for Learning from Preference Feedback | OpenReview, accessed March 22, 2026, [https://openreview.net/forum?id=JMBWTlazjW](https://openreview.net/forum?id=JMBWTlazjW)  
31. Unpacking DPO and PPO: Disentangling Best Practices for Learning from Preference Feedback \- NIPS papers, accessed March 22, 2026, [https://proceedings.neurips.cc/paper\_files/paper/2024/file/404df2480b6eef0486a1679e371894b0-Paper-Conference.pdf](https://proceedings.neurips.cc/paper_files/paper/2024/file/404df2480b6eef0486a1679e371894b0-Paper-Conference.pdf)  
32. “Step by Step” Journey To Reasoning LLMs | by Abhishek Bairagi | Towards AI, accessed March 22, 2026, [https://pub.towardsai.net/step-by-step-journey-to-reasoning-llms-d4f45fcfb080](https://pub.towardsai.net/step-by-step-journey-to-reasoning-llms-d4f45fcfb080)  
33. A Tutorial on LLM Reasoning: Relevant Methods behind ChatGPT o1 \- arXiv.org, accessed March 22, 2026, [https://arxiv.org/html/2502.10867v1](https://arxiv.org/html/2502.10867v1)  
34. Learning to reason with LLMs | OpenAI, accessed March 22, 2026, [https://openai.com/index/learning-to-reason-with-llms/](https://openai.com/index/learning-to-reason-with-llms/)  
35. Understanding Reasoning Models & Test-Time Compute: Insights from DeepSeek-R1, accessed March 22, 2026, [https://medium.com/@cch.chichieh/understanding-reasoning-models-test-time-compute-insights-from-deepseek-r1-d30783070827](https://medium.com/@cch.chichieh/understanding-reasoning-models-test-time-compute-insights-from-deepseek-r1-d30783070827)  
36. Inference-Time Scaling: The New Training Frontier for AI Reasoning \- Introl, accessed March 22, 2026, [https://introl.com/blog/inference-time-scaling-research-reasoning-models-december-2025](https://introl.com/blog/inference-time-scaling-research-reasoning-models-december-2025)  
37. DeepSeek R1 vs OpenAI o3 vs Gemini 3: Reasoning Model Benchmarks \[2026\] \- 超智諮詢, accessed March 22, 2026, [https://www.meta-intelligence.tech/en/insight-reasoning-models](https://www.meta-intelligence.tech/en/insight-reasoning-models)  
38. What is test-time compute and how to scale it? \- Hugging Face, accessed March 22, 2026, [https://huggingface.co/blog/Kseniase/testtimecompute](https://huggingface.co/blog/Kseniase/testtimecompute)  
39. Let's Verify Step by Step | OpenAI, accessed March 22, 2026, [https://cdn.openai.com/improving-mathematical-reasoning-with-process-supervision/Lets\_Verify\_Step\_by\_Step.pdf](https://cdn.openai.com/improving-mathematical-reasoning-with-process-supervision/Lets_Verify_Step_by_Step.pdf)  
40. Process vs. Outcome Supervision \- Emergent Mind, accessed March 22, 2026, [https://www.emergentmind.com/topics/process-vs-outcome-supervision](https://www.emergentmind.com/topics/process-vs-outcome-supervision)  
41. Process Supervision for Chain-of-Thought Reasoning via Monte Carlo Net Information Gain, accessed March 22, 2026, [https://arxiv.org/html/2603.17815v1](https://arxiv.org/html/2603.17815v1)  
42. Let's Verify Step by Step, ORM vs PRM | by Yanan Chen \- Medium, accessed March 22, 2026, [https://medium.com/@yananchen1116/lets-verify-step-by-step-orm-vs-prm-613ecffb59ab](https://medium.com/@yananchen1116/lets-verify-step-by-step-orm-vs-prm-613ecffb59ab)  
43. Mechanisms for test-time compute \- Innovation Endeavors, accessed March 22, 2026, [https://www.innovationendeavors.com/insights/mechanisms-for-test-time-compute](https://www.innovationendeavors.com/insights/mechanisms-for-test-time-compute)  
44. Human-in-the-Loop, Human-on-the-Loop, and LLM-as-a-Judge for Validating AI Outputs, accessed March 22, 2026, [https://kili-technology.com/blog/human-in-the-loop-human-on-the-loop-and-llm-as-a-judge-for-validating-ai-outputs](https://kili-technology.com/blog/human-in-the-loop-human-on-the-loop-and-llm-as-a-judge-for-validating-ai-outputs)  
45. Human-in-the-Loop Review Workflows for LLM Applications & Agents \- Comet, accessed March 22, 2026, [https://www.comet.com/site/blog/human-in-the-loop/](https://www.comet.com/site/blog/human-in-the-loop/)  
46. The Truth About Synthetic Data: Why Human Expertise is Critical for LLM Success \- Unite.AI, accessed March 22, 2026, [https://www.unite.ai/the-truth-about-synthetic-data-why-human-expertise-is-critical-for-llm-success/](https://www.unite.ai/the-truth-about-synthetic-data-why-human-expertise-is-critical-for-llm-success/)  
47. Human Data is (Probably) More Expensive Than Compute for Training Frontier LLMs | by Daniel Kang | Medium, accessed March 22, 2026, [https://medium.com/@danieldkang/human-data-is-probably-more-expensive-than-compute-for-training-frontier-llms-3c916ef309e4](https://medium.com/@danieldkang/human-data-is-probably-more-expensive-than-compute-for-training-frontier-llms-3c916ef309e4)  
48. An economic report on the human expertise fueling frontier AI \- Labelbox, accessed March 22, 2026, [https://labelbox.com/blog/an-economic-report-on-the-human-expertise-fueling-frontier-ai/](https://labelbox.com/blog/an-economic-report-on-the-human-expertise-fueling-frontier-ai/)  
49. Beyond Scarcity: How LLM-Driven Synthetic Data Generation is Reshaping AI \- Towards AI, accessed March 22, 2026, [https://towardsai.net/p/machine-learning/beyond-scarcity-how-llm-driven-synthetic-data-generation-is-reshaping-ai](https://towardsai.net/p/machine-learning/beyond-scarcity-how-llm-driven-synthetic-data-generation-is-reshaping-ai)  
50. Why Synthetic Data Is Taking Over in 2026: Solving AI's Data Crisis \- Humans in the Loop, accessed March 22, 2026, [https://humansintheloop.org/synthetic-data-ai-models/](https://humansintheloop.org/synthetic-data-ai-models/)  
51. 10 Strategies for Scaling Synthetic Data in LLM Training \- DZone, accessed March 22, 2026, [https://dzone.com/articles/scaling-synthetic-data-llm-training?fromrel=true](https://dzone.com/articles/scaling-synthetic-data-llm-training?fromrel=true)  
52. Synthetic Data and Human-in-the-Loop: Balancing Automation with Human Expertise, accessed March 22, 2026, [https://www.dataforce.ai/blog/synthetic-data-and-human-in-the-loop-balancing-automation-with-human-expertise](https://www.dataforce.ai/blog/synthetic-data-and-human-in-the-loop-balancing-automation-with-human-expertise)  
53. MMLU-Pro Explained: The Advanced AI Benchmark for LLMs | IntuitionLabs, accessed March 22, 2026, [https://intuitionlabs.ai/articles/mmlu-pro-ai-benchmark-explained](https://intuitionlabs.ai/articles/mmlu-pro-ai-benchmark-explained)  
54. LLM Benchmarks Compared: MMLU, HumanEval, GSM8K and More (2026), accessed March 22, 2026, [https://www.lxt.ai/blog/llm-benchmarks/](https://www.lxt.ai/blog/llm-benchmarks/)  
55. Open Source LLM Leaderboard 2026: Rankings, Benchmarks & the Best Models Right Now \- VERTU® Official Site, accessed March 22, 2026, [https://vertu.com/lifestyle/open-source-llm-leaderboard-2026-rankings-benchmarks-the-best-models-right-now/](https://vertu.com/lifestyle/open-source-llm-leaderboard-2026-rankings-benchmarks-the-best-models-right-now/)  
56. LLM Guardrails: Securing LLMs for Safe AI Deployment \- WitnessAI, accessed March 22, 2026, [https://witness.ai/blog/llm-guardrails/](https://witness.ai/blog/llm-guardrails/)  
57. LLM guardrails: Best practices for deploying LLM apps securely \- Datadog, accessed March 22, 2026, [https://www.datadoghq.com/blog/llm-guardrails-best-practices/](https://www.datadoghq.com/blog/llm-guardrails-best-practices/)  
58. Evaluating the Robustness of Large Language Model Safety Guardrails Against Adversarial Attacks \- arXiv, accessed March 22, 2026, [https://arxiv.org/html/2511.22047v1](https://arxiv.org/html/2511.22047v1)  
59. How do guardrails affect LLM performance? \- Milvus, accessed March 22, 2026, [https://milvus.io/ai-quick-reference/how-do-guardrails-affect-llm-performance](https://milvus.io/ai-quick-reference/how-do-guardrails-affect-llm-performance)  
60. How Good Are the LLM Guardrails on the Market? A Comparative Study on the Effectiveness of LLM Content Filtering Across Major GenAI Platforms \- Unit 42, accessed March 22, 2026, [https://unit42.paloaltonetworks.com/comparing-llm-guardrails-across-genai-platforms/](https://unit42.paloaltonetworks.com/comparing-llm-guardrails-across-genai-platforms/)  
61. Researchers Discover Major Security Gaps in LLM Guardrails \- Infosecurity Magazine, accessed March 22, 2026, [https://www.infosecurity-magazine.com/news/major-security-gaps-llm-guardrails/](https://www.infosecurity-magazine.com/news/major-security-gaps-llm-guardrails/)  
62. An efficient, reusable framework to evaluate AI safety \- JHU Hub, accessed March 22, 2026, [https://hub.jhu.edu/2026/03/11/efficient-ai-safety-testing/](https://hub.jhu.edu/2026/03/11/efficient-ai-safety-testing/)  
63. What is LLM Guardrails? Types & Importance \- Deepchecks, accessed March 22, 2026, [https://deepchecks.com/glossary/llm-guardrails/](https://deepchecks.com/glossary/llm-guardrails/)  
64. The Best Open-Source LLMs in 2026 \- BentoML, accessed March 22, 2026, [https://www.bentoml.com/blog/navigating-the-world-of-open-source-large-language-models](https://www.bentoml.com/blog/navigating-the-world-of-open-source-large-language-models)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAZCAYAAADuWXTMAAAA20lEQVR4Xt3SsQpBURzH8YOBxKBkYzBYpJSUbFZlQXkBRYqNsngAT+ANDMobSNltBl5AGU0W4ffX77ru5dLtLPKtz3KO3+B2lPq70tSDPkUtv/iQ67FciimMKQYJkvMmWQrBhoa2O6Mk7Mn7fKE1nsCCnPLAhYpyEKEztMipLFwpJwda4yrJWL6scGoEBwrIgda4TCfwk70gbaFN94yHcYQa1ZX5qlIwpw43j7TGRhVY0gwatIYSST56yfhvecjQSpkfcgBheklr/K6dMh9G13b3tTgUyHVa4x/sBi4WPs7nIMEhAAAAAElFTkSuQmCC>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAYCAYAAAD3Va0xAAAAwElEQVR4Xu3TvQpBYQDG8TelRHEBlrMpHzfgI5uYlZLJZOMaLAaXYFFKrEyuwe4OLAYpi6LkeesfxzmRcjb+9VvO+/YM53SM+ZkclKWIkiRgSyMvBUQ5u+fg66EUJrJF3TwPDbGWLiKc+ZrLCO7a0sJHBTa0kwbi0kfGfeldWVylAvsuZvi4wIZ6OEgTduyC5OPq+5awn9fdBgPP85cFMhSWI6qesw72EoOvGqZyxtg8fpeQLHCSFXLGU2BD/362Gwi8PG726LwNAAAAAElFTkSuQmCC>

[image3]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAZCAYAAAA4/K6pAAAArElEQVR4XmNgGBZAGIptgdgSiq1RVECAKgNEDQjbAzEzFFNugDQUTwbiD1DsDdGDAhyA+DYUZwIxExTDgQ0Qf4dibCAOiC2gGCug2AA5IP4PxaJI4gJQ3IokhhWwAPFfKDZCEm+EYhEkMayAYgNA4AkU+zNADAHhZCgmClBswHEozgPiiVCMEd/4wEoovgfExlBMEqDYgC4onoQuQSyQhWJudAliAcUGjIKBAACphymS16D1ygAAAABJRU5ErkJggg==>

[image4]: <data:image/png;base64,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>

[image5]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABMAAAAZCAYAAADTyxWqAAAA5UlEQVR4XuXRMWoCQRSA4YkYbERJELQLFipoZ5dOm9iJCBEbwUYRwcoDaJXCIlUKBXshRc6QM9h4AbHKCax8g/+us1qEcacRf/iKfbO8Ykapu6+MNlLBY7ucLqtij+fgsV0lrBGq0MsyeBVDfMGqpvhARfzhHVY5WVbAVsSg2yENXQsDvi9yumyClTHLiw3M6uiezf28ZWNjNhILdPEgPlE05jll5HSZd2dz0cNMfKMP3S8aooYsZ4EiIg6d+Ri6pPjBUrzgyfjHz+my/3pTp3vqiCkS3g82RdXxETTdI67K6bIb7gAoRTrhZnsP/gAAAABJRU5ErkJggg==>

[image6]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACoAAAAYCAYAAACMcW/9AAABwUlEQVR4Xu3WSyhEURzH8ev9jLxWiKTkEXkkWVCShZJnrMlCsRN5LCgrG9koGywlNpZWFjayxc6CjTxW9orff/yOOfOfuTXXpeaWb30Wzplxz505c+91nP8SvxRIJq+l64F4qqc5mKfiiFfEbhsyyWuLUEdxl9ALlYWIfVilQiijY5gm3QT16wkPycmdkOs2yIVbGlZzpiZ4JHsP5sMe+U2OLdb0hCkwC92Fc3IrCz6o0xpfgCXSdZC819QM1aQroks9UUDvMEZutTrhhbZY4/JJjpCdfDKzdOd8/TBFO9xTDV+re4AkChWYhZoDyMHdvg7TCjxThjUu26WB7Aahi24glST5akU3/9bJXAWFksuJkIVmk86Mv8AM2Z1BI+nWadMaK4VXMgvXXUEVhQrMQs1F/g16yC4NjmhDzZm2HPf9fUF91pjs2QPqhXKyMycRdSIDcE3jTvgOdAiT5NYULJOdPKA8kX15kv8rdzkxao1LJSTX85gFZqGS2YttUEtRH32MKuGUdG77Po905plBX+p+LfMjG9ITHsqBHfqzArNQkzyPyn6092S8ybNCxEX+L/u+5f0gP+/1nJ+D+XlvYvQJ4BJ7hTJnPi8AAAAASUVORK5CYII=>

[image7]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAZCAYAAABD2GxlAAABkklEQVR4Xu3VvytFYRzH8Qf5GWHwI0oUxWKRHyGL/CglA7LeolCUlcGfYDGRQSx+RJlMKKvBwMaA3SKJEt9v5/PwPU/32z3HTT3DfddreZ7Tvd865zzHmEz+lQtRy4PYtcMSmYPC0BXhamAZ3LIE2RBMOOsp83JA+ye7ZBGKSCuckj5wW4MS4BqBB76CDuy5bZFqSFo5uYNeZ8+WIMcg6yfTIKsHHvIRtAEbyAEkzfsBt8kRaHWTNygQ6+ekGbQeQBuQu4XQc1oBn2QAtGbIK2SL9SeT+riIMuAZ1MlF7wechC9SCVr7JniTGcfHDrv/uULPDtjpbog2YFguej/gKLyTHHCz59mH+T3AOXtb+c1PVZQBN2FELlbBC2kDWSm5hClnz3ZD8kHLDtjlboguoEUuej+gbZxcwxhZgD0yCFqHJvhR94d7gD+Bz3BCZsHNfijkGRuqGPgoaILQoamUIPPw1/i/VkHN+wHTaQfKIG7rJri16u1Nt1pYgajxkcJCZ99/5P2ANn5mozy3trjXZ4rVN5WaemysXKFBAAAAAElFTkSuQmCC>

[image8]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAYCAYAAAAlBadpAAAArUlEQVR4Xu3QsQpBUQDG8RMRKVlZiBcwWFiVgdmkjMwWi1ewmpjkHZSdRR7HJPHd48+9XV3RGZT86zed+51T15ifq4KhTFCWBOr+p899PM5hIWs0pIip7NFjY8vIDkvjvxAsJUfkgwdO47ls8aoVbN4NnpOM8HZO4w4uUkJUSYnB1sZZsohqLGnYnMZxHKSPcE20wgf3qrLBTLoYmNsocujlNA5WkBoef/bfN7sCVeoqKfmzuY0AAAAASUVORK5CYII=>

[image9]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAYCAYAAAD3Va0xAAAAxUlEQVR4Xu3SPQ4BQRjG8Zf46pUUopRIFCoh4QAKER13kLiAlhA30OnEISQ6rVrnCgoRnoln1uzsZBvTrX/yK3Zm8mazsyKJqUI96FIm2P3UMrSpEDohHgfVaAt3GodOiIzoClPKh04YrWFBZ2uvSHNr3dnPg1K0hDI9oEOqIelnZ3WaGGs7OJBKv2k2OOHI2yB9CyVjrQlPqsKGYlMfWbE70h5mFJuXQTlYkd2AXtCgSH26wI3U9Zql6STfXySSt0H/EtsbMbYziX9g7wAAAAAASUVORK5CYII=>

[image10]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAAYCAYAAAAcYhYyAAAAs0lEQVR4Xu3SMQ4BQRiG4VVItGqlEhG1Ap1K4gYuIBFad1BQ6SRKEj1ahRM4hFaUfCPvbvjtanaqjTd5mpmdf3eTCYJMV0bnTVtaqEVP/sjLkAp2ckJP+ljJGkXOJLaXEWxbjO2GLdWQPG5Sh20C96LYmrhKDrYFDnYjzMuQKdw/J3XBwKxHHTG0G+TuyhlxX/kq9ZCC3FE1e+GNdYcb+KiLjTwwlxnc+hIlznzlZci/TPcE4n82hDCW0ZAAAAAASUVORK5CYII=>

[image11]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAE0AAAAYCAYAAAC/SnD0AAACOUlEQVR4Xu3XS6hNURzH8eWtEK5XknRR8pog5Z2JpJAUkRgwkNKVV4qSUN5FiilKGUjm5DFhgKFSSorMTWQg/r/Od9297qp1ztrlXLpnfetT9+697+t/9157b+c6r5WBVHuw3qxDx3bRTMFWswlxj3HMdKFja8vQurHWrMHgPkc4txrLzAoM6XPEv0mX22EcMKMx00zDq96jnVtgLiDuNHaasUhWhtao1tDm4575gS3B/kFmFz6Z/YgH218tNM+hS28eFpv7+GzG4I2+iOaaO4jbjBHmKVp2xVzHy2jfLPRE2/szP5xvZh/iNiI8ux4EH2uwxxGmM9CfDOodhvUekagMrcbQdJmJrnM/nF9mEdRe6JvnpEtatOYsRbwG+nVjg6t+h1T62g84E+0Lm4GzwbYdrrFOySkzB/rbLmGcOQItQyeQTNOX7cG2R+Yu1FXkdg5anG9BZ+9E6JZ/A0tcNeRU28xv5P7jwiZBN4lUOquk6aOGrwytUa2hHcXkYJseO35iqrmGnEa56pUkTEN8C62bddJ6+xHNGom2p19I4vxi+NBVa1pOy131LBemdUmPAnIw2teqy+Y1UulRoeVa9LcqQ6uZfpC/g8TthtaRbuSky/MQwvTgeBNfzCrkNN18h57yw/x6qHfG8WhL/qX1vfkK/VFhw/Ei2p6TFm457xq3fzkZ7NejyBPcNkPRLP9W8sxVZ5Q+989Xs6tD21MZ2n+cbvH+Vp5qQrwhI/++PGAGVSqVSqXSwOsPFZCkmWKfjmEAAAAASUVORK5CYII=>

[image12]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEwAAAAYCAYAAABQiBvKAAACMklEQVR4Xu3XTYhNYRjA8Zd8hUkKWXFC8i0fNYV8J0ms5KPIysjK1wyZsEA+IoVSbERNQyxISpLFxMLGhiQbSbKwMgtLnuee/3vP29M9596T7pi6779+i7nvuXPvPOfe95xxrrVageV2IWgvNor1aMkuiknY7tKBKNsTHBXj0ZI1ZWAJ1gRWi1VYynGDLX1vR9AhRmO2mIA31aOdWyTOwHYau0QbcksQB9bgwGahR7zHFrEV18VTJOlT/lsLRR/Ouey9t4tefBEj8LbyrLQF4jZs/m8dJV6gbo9c/hm4hFt2YYCaix8uu6LZduJ58JgO0KdDPYSweWIftHcYWj0ipziwtLoDG4KfLtvDbP4j+80u5DQHa122t4Tp12UdCq9I0jDxGSfNWpgfalfwmO5JfpCnxAwsERegr+/3wt2iE7npvqB+i5GwHcR3u1CjbeIsToiP0Nfwe849sRJ2mLYd4g/0uWWbiLF2IWg46p28SnFgJQfmv9cv7ULQM5y3CzU6YH7ejK/iAWqdlLyuiE8oSq9wqun5W4Zuu0DTXXqpVkVnSTdJddgu0EOXfrJUmS6L18hrjMv2oaYXB1Yi/d72Y5lZW4w+sQmNZAc/E3fEB+ideaNNEb8w2az5k3TcpSez6IT+Uxtw32Ub6k1xFXr/chdlN1r9F+Qajokb0P1lKh677PcnlWcVtwevXHrboPQWYD+S6pFNKg5skOUv00VfkXHQG9Myzcc0uxCLxWKxWGyg+ws6zaZ/q+XMjAAAAABJRU5ErkJggg==>

[image13]: <data:image/png;base64,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>

[image14]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAZCAYAAADuWXTMAAAAtElEQVR4Xu3SPQ4BQRiH8fV1CqKgkihoxBHoJahcQaJyBQWNUIhKxQHECXRuoNJq9fwneWaSnY1Edjo8ya/ZN+8kO7tR9BWV0P5AhR1X0HITe7lhIH2M5IQFO4kOsoZfHWN/YEu1nMFdejANUZMyWsxcDTxli41cYQ5+W9DyBBfJoyg7mKpIHBS0fMTMe25fJysrxCrIAx1vZptG8a/gSrXchfkxzC3bm55jKWeYG8/h34/0AiO9Nb8Ia7tOAAAAAElFTkSuQmCC>

[image15]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFAAAAAYCAYAAABtGnqsAAACgklEQVR4Xu3YS6hNURgH8O/m/bweJQPyiLyKEhl4XpFLorxS170lpCQDlGek6JYkGSAMUAyUGEgZmImZTGTgNWNGeQzcEt+/9V9nr/21s/e2tzqx/vWre9dae59zv7P3d9a+IjExMf9BOmmanSiRcaotsCQwh1rc0qZKK+1Ua6h3akWBxAJWKOBY9ZXWm7kymaqu0QtJ3gwcp5dqJDVDJqtuGqT20q5wUV7OqTdU6sCM3KRTZhxXHnxRXdQMOSnJe0O20pnGigKJBfzDArbTOvWQTqRWlM97WmrGN9MrNYrKpp9aSVVbwCzaKK71wET1lHBr/zb91XlC/JVzqbGifPAmftARtY9w3rM0orG6eLbTQTWdbqsFNF9NoKLxvW6KukFX1QXKTSxgxQIeVcsJL+xPcjdcVDLon48ozDD1jDrMXF5mSnJsmLWStJ3DZq5I/K7A5jnhGzkzk+iy2h1A4eBJsrR07oj7YMDmHt23EznBMQcozEL1mRabubz0FVd0W/jh6jvh58zEAlYoIHbX6HGAb7Qwvs+8M+NjaIUZD9OLPorrRxAGPauHNpi5eTTDjPs8ELe5txv8VeothcHftYn6mDkfFPwYhdkmrrdCKngxeK0+0OxgHn3wMX2TpJGi4OhZgKeUwRRmmbpFP9VFwhfGdboiybbBxn+geO2szJXkPFvE9VnYIUm/whWPPgu4uz4RtjtZOSRunwd7xJ0L8Cg3gFKJBUyndAHrCC73rALWldN2ICNDze/4gGGgGV9Ni8y4T/iwgKLjtrctrba0km3idaWNcBfUlW6ywdYE9tuJv5lYwIrBkwMMsRM1ZTzVlRZx/5cEG38xjLYTMTEx/2x+AXeWyNM4ce9MAAAAAElFTkSuQmCC>