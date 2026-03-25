# Evaluation Data

Evaluation data consists of carefully constructed test sets used to measure a language model's capabilities, kept strictly separate from training data. It serves the same purpose as board exams in medicine: testing whether the model has genuine understanding rather than mere memorization of training examples.

## How It Works

Evaluation data must satisfy several requirements to be useful. First, it must be held out from training. If a model has seen the evaluation questions during pre-training, its performance on those questions reflects memorization, not capability. This is the data leakage or benchmark contamination problem, and it is pervasive.

Benchmark contamination occurs when evaluation datasets inadvertently appear in pre-training corpora. Web crawls that form the basis of pre-training data may include pages that discuss, reproduce, or reference benchmark questions and answers. A model that scores 90% on a contaminated benchmark may perform at 70% on genuinely unseen questions testing the same skills. Detecting contamination is difficult because pre-training datasets are often undisclosed or too large to audit exhaustively.

To address contamination, modern benchmarks employ several strategies. Private test sets keep questions hidden from the public. Canary strings, unique text sequences embedded in test sets, can be checked against model outputs to detect memorization. Dynamic benchmarks generate new questions programmatically. Human evaluation eliminates the fixed-dataset problem entirely by using fresh questions for each assessment.

Evaluation must test understanding, not memorization. A model that has memorized the answer to "What is the capital of France?" tells you nothing about its geographic reasoning ability. Well-designed evaluations test generalization: can the model apply its knowledge to novel problems it has never seen? This requires multiple evaluation formats, including multiple choice, free-form generation, code execution, and multi-step reasoning, because a model may perform well in one format and poorly in another.

Evaluation datasets are typically small compared to training data, often just hundreds to thousands of questions, but each question is carefully validated for correctness, clarity, and difficulty calibration.

## Medical Analogy

Evaluation data is the board exam question bank. Medical licensing exams are developed by separate organizations, kept secure, and regularly refreshed precisely because if students could access the exact questions in advance, passing the exam would prove nothing about their clinical competence. The exam tests whether the student can apply medical knowledge to novel patient scenarios, not whether they memorized a specific set of answers.

## Why It Matters for Enterprise AI

Evaluation is where most enterprise AI initiatives lose their way. The over 80% of AI deployments showing no meaningful EBIT impact often have a common root cause: nobody measured the right thing. Off-the-shelf benchmarks tell you whether a model is generally capable. They tell you nothing about whether it can handle your specific use cases. The $252B invested in AI produced models that score impressively on public benchmarks, but your business runs on domain-specific tasks that those benchmarks do not cover. Building your own evaluation sets, drawn from your ground truth and graded against your quality standards, is the single most important step in enterprise AI deployment. Without it, you are flying blind. Your codified craftsmanship includes knowing what "good" looks like in your domain. Capture that knowledge as evaluation data, and you have a repeatable, objective way to measure whether your AI investment is delivering value or just generating impressive-sounding nonsense.

## Key Technical Details

- Held-out requirement: evaluation data must not appear in training corpora
- Benchmark contamination: pre-training data inadvertently includes test questions
- Detection methods: canary strings, n-gram overlap analysis, membership inference
- Private test sets: questions never publicly released (e.g., LMSYS arena)
- Dynamic benchmarks: programmatically generated to resist memorization
- Multiple formats needed: MCQ, free-form, code execution, multi-step reasoning
- Typical size: hundreds to thousands of carefully validated questions
- Inter-annotator agreement: human evaluators must agree on correct answers
- Difficulty calibration: questions should span easy to expert-level

## Related Terms

- [Benchmarks](benchmarks.md)
- [LLM as a Judge](llm-as-a-judge.md)
- [Training Data](training-data.md)
- [Pre-training](pre-training.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
