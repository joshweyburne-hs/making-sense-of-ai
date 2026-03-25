# Benchmarks

Benchmarks are standardized tests that measure language model capabilities across defined tasks, enabling comparison between models. They serve the same function as board exams in medicine: a common yardstick that provides a shared vocabulary for discussing competence, while acknowledging that no single test captures the full picture.

## How It Works

The LLM benchmark landscape includes several key assessments, each targeting different capabilities.

**MMLU (Massive Multitask Language Understanding)** was the flagship knowledge benchmark, covering 57 subjects from elementary math to professional law. Frontier models have saturated it, with top scores exceeding 90%. **MMLU-Pro** replaces it with harder questions requiring genuine reasoning, 10 answer options instead of 4 (reducing random guessing from 25% to 10%), and integrated chain-of-thought prompting.

**GPQA Diamond (Graduate-Level Google-Proof Q&A)** tests PhD-level science knowledge with questions specifically designed to resist internet searching. Domain experts achieve roughly 65% accuracy; non-experts with Google access score around 34%. This makes it a strong test of genuine expertise.

**AIME (American Invitational Mathematics Examination)** is a competition math benchmark that tests multi-step mathematical reasoning. Problems require creative problem-solving, not formula application. It has become a standard measure of reasoning capability, with frontier models now solving 70-80% of problems.

**HumanEval** tests code generation with 164 Python programming problems. Models must write functioning code, not just code that looks plausible. Pass@1 (correct on first try) is the standard metric.

**SWE-bench Verified** tests real-world software engineering by asking models to resolve actual GitHub issues from popular repositories. Models must understand codebases, identify relevant files, and generate correct patches. This is significantly harder than isolated coding problems.

**LMSYS Chatbot Arena** sidesteps fixed benchmarks entirely. Real users chat with two anonymous models simultaneously and vote for the better response. The resulting Elo rating system reflects human preference on open-ended, real-world interactions. It is widely considered the most reliable indicator of overall model quality.

Benchmark saturation is a persistent challenge. As frontier models approach ceiling scores on existing benchmarks, those benchmarks lose their ability to differentiate. This drives a continuous cycle of creating harder benchmarks. Domain-specific professional benchmarks like **BankerToolBench** (financial tool-use scenarios) represent the next evolution: testing capabilities in contexts that matter for specific industries rather than general academic knowledge.

## Medical Analogy

Benchmarks are USMLE Steps 1, 2, and 3. Step 1 tests foundational knowledge, Step 2 tests clinical application, Step 3 tests independent practice readiness. No single exam tells you whether someone will be a good doctor, but together they provide a structured assessment. Similarly, no single benchmark captures full model capability, but the suite provides a multidimensional profile.

## Why It Matters for Enterprise AI

Benchmarks help you make informed decisions, but the benchmarks that matter most for your organization probably do not exist yet. The $252B invested in AI produced models that excel on public benchmarks, yet over 80% of deployments show no meaningful EBIT impact. Why? Public benchmarks test general capabilities. Your business depends on domain-specific performance. A model that scores 95% on MMLU may fail catastrophically on your compliance review workflow. Building internal benchmarks, tests grounded in your ground truth that measure performance on your actual use cases, is where codified craftsmanship becomes measurable. Domain-specific benchmarks are your scoreboard for whether AI is delivering real value. Without them, you are optimizing for someone else's definition of success.

## Key Technical Details

- MMLU: 57 subjects, saturated at 90%+; being replaced by MMLU-Pro (10 options, reasoning focus)
- GPQA Diamond: PhD-level, Google-proof; expert accuracy ~65%
- AIME: competition math; tests multi-step creative reasoning
- HumanEval: 164 Python problems; Pass@1 metric
- SWE-bench Verified: real GitHub issues; tests practical software engineering
- LMSYS Chatbot Arena: Elo-rated human preference; 1M+ votes collected
- Benchmark saturation: frontier models approach ceilings, reducing differentiation power
- Domain-specific benchmarks (BankerToolBench) reflect real professional requirements
- Contamination risk: models may have seen benchmark questions in training data

## Related Terms

- [Evaluation Data](evaluation-data.md)
- [LLM as a Judge](llm-as-a-judge.md)
- [Alignment](alignment.md)
- [Pre-training](pre-training.md)

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
