# Board Exams: Measuring What Models Know

*Part 4 of the series: [Understanding LLMs Through the Medical Training Analogy](00-overview-the-journey.md)*

**Terms covered:** Evaluation Data, Benchmarks, LLM as a Judge

*For a deeper technical dive, see [Evaluation Data](Research_Docs/Terms/evaluation-data.md), [Benchmarks](Research_Docs/Terms/benchmarks.md), [LLM as a Judge](Research_Docs/Terms/llm-as-a-judge.md).*

---

## The Old Tests Don't Work Anymore. You Need Yours.

Frontier models now score above 90% on MMLU — the benchmark the industry treated as the gold standard for years. When every top model aces the same test, the test stops telling you anything useful. This is **benchmark saturation**, and it means the generic leaderboards that vendors wave around in sales decks are increasingly meaningless for your buying decisions.

The models that matter for your organization aren't the ones that top public benchmarks. They're the ones that perform against *your* definition of quality, grounded in *your* domain expertise. Understanding how evaluation actually works tells you exactly what to demand.

---

## The Medical Scenario

After years of medical school and residency, a doctor faces board certification. The USMLE doesn't care where you went to school or who your attending was. It presents standardized questions that test whether you understand medicine well enough to practice safely.

But board exams are just one piece. There are clinical competency evaluations where senior physicians observe you with real patients. Peer reviews where colleagues assess your judgment. Case conferences where your reasoning is dissected by experts.

Each method measures something different. Standardized exams test breadth. Clinical evaluations test practical skill. Peer review tests judgment. Together, they build a picture of whether a doctor is ready.

LLMs face the same gauntlet — and understanding how models are evaluated is critical for anyone who needs to choose, trust, or deploy one.

---

## Evaluation Data: The Exam Questions

Every good exam has one golden rule: the questions must be different from the study materials. A student who memorizes every practice test but can't handle an unfamiliar question hasn't learned — they've memorized.

**Evaluation data** is the carefully separated set of questions and tasks used to test a model's capabilities *after* training. This data is deliberately kept away from the training process. If a model trained on the same data it was tested on, scores would be meaninglessly inflated — the AI equivalent of seeing the answer key before the exam.

Creating good evaluation data requires real thought:

- **It must be separate from training data.** Responsible AI labs "decontaminate" their benchmarks by ensuring no test questions leaked into training sets. This isn't trivial — when your training data includes much of the internet, benchmark questions published online might accidentally be included.

- **It must test understanding, not memorization.** A good evaluation question requires the model to reason, synthesize, or apply knowledge — not just recall.

- **It must cover the right dimensions.** Just like medical boards test across specialties (cardiology, neurology, pharmacology), evaluation data should test across capabilities (factual knowledge, reasoning, code generation, creative writing, safety).

Evaluation data takes many forms: multiple-choice questions, open-ended prompts, coding challenges, mathematical problems, translation tasks. No single set gives you the full picture — which is why the industry uses benchmarks.

> **Simplification Note:** There's an ongoing problem called "benchmark contamination" or "data leakage" — where evaluation questions accidentally appear in training data, artificially inflating scores. Like a medical school accidentally including real board questions in practice tests. Interpreting benchmark scores requires awareness of this possibility.

---

## Benchmarks: The Standardized Board Exams

The USMLE lets hospitals compare doctors from different programs on a level playing field. A score of 250 from one program means the same as a 250 from another. That standardization is what makes it useful.

**Benchmarks** serve the same purpose for LLMs — standardized tests enabling apples-to-apples comparison across models. When a company announces "our model scores 90% on MMLU," they're citing a specific, verifiable test.

Here are the benchmarks that appear most often in model announcements:

**MMLU (Massive Multitask Language Understanding):** The broadest "board exam" for LLMs — 57 subjects from abstract algebra to world religions, with multiple-choice questions at high school through professional level. Current frontier models score above 90%, which is why it's losing diagnostic value. **MMLU-Pro** was introduced as a harder replacement: 10 answer options instead of 4, emphasis on multi-step reasoning, and questions designed to resist educated guessing. When you see vendors citing MMLU scores, ask if they mean the original or Pro version. The gap between the two tells you more than either score alone.

**GPQA (Graduate-Level Google-Proof Q&A):** Questions so hard that PhD-level researchers only answer about 65% correctly, and answers can't be Googled. The equivalent of the most brutal oral board exam by a panel of senior specialists.

**HumanEval / SWE-bench:** Coding benchmarks where models must write working code that passes tests (HumanEval) or fix real bugs in open-source projects (SWE-bench). Like evaluating a surgeon's operating skill, not just their anatomy knowledge.

**MATH / GSM8K:** Mathematical reasoning benchmarks from grade-school word problems to competition-level mathematics. Tests logical thinking, not memorization.

**LMSYS Chatbot Arena:** The most human-centric evaluation. Real users have blind conversations with two models and vote on which they prefer. Like a patient satisfaction survey — it measures subjective interaction quality, not just technical accuracy. Over two million human preferences collected.

**Domain-Specific Professional Benchmarks:** This is where evaluation gets genuinely interesting for enterprises. **BankerToolBench**, for example, evaluates AI on 500 real investment banking tasks — not generic finance questions, but actual IB workflows evaluated against standards set by senior bankers. This is the direction evaluation is heading: not "can it pass a generic test?" but "can it perform at the level your best people expect?" Every domain needs its own version of this.

Each benchmark reveals something different. A model might score brilliantly on MMLU but struggle on HumanEval. Another might ace math but rank poorly on Chatbot Arena. No single number tells the whole story.

> **Simplification Note:** Benchmark scores should be interpreted with healthy skepticism. MMLU uses multiple-choice format that doesn't reflect real-world usage. Models may have "seen" benchmark-like questions during training. Benchmarks can be gamed through prompt engineering. And benchmark performance doesn't always correlate with usefulness for a specific task. Necessary but insufficient — like how a perfect USMLE score doesn't guarantee good bedside manner.

---

## LLM as a Judge: Peer Review at Scale

Some aspects of a doctor's work can't be evaluated by standardized tests. The quality of a surgical handoff note. The clarity of a patient explanation. The appropriateness of a treatment decision given specific context. Medicine relies on peer review for these — experienced doctors evaluating other doctors.

**LLM as a Judge** applies this same principle to AI. Instead of — or in addition to — human evaluators, a powerful LLM evaluates the outputs of other models or systems.

How it works in practice:

1. **A model generates a response** to a question or task.
2. **A separate, typically more powerful LLM** reviews that response and scores it on criteria like accuracy, helpfulness, relevance, safety, and completeness.
3. **The scores are aggregated** across thousands of evaluations to build a picture of model quality.

Why use an LLM instead of humans? Scale and consistency. Human evaluation is the gold standard, but it's slow (thousands of responses take weeks) and expensive (skilled evaluators cost real money). An LLM judge evaluates thousands of responses in minutes — fast, consistent, and surprisingly accurate.

Research shows strong LLM judges agree with human evaluators roughly 80-85% of the time — comparable to agreement between two human evaluators. Not perfect, but practical for rapid evaluation.

**Process vs. Outcome Supervision:** An emerging distinction in LLM-as-Judge evaluation is whether you judge the *process* or just the *outcome*. **Outcome Reward Models (ORMs)** evaluate only the final answer — did you get it right? **Process Reward Models (PRMs)** evaluate each reasoning step along the way — did you get there correctly? PRMs are more expensive but catch models that arrive at right answers through wrong reasoning — a critical distinction when you need to trust the logic, not just the result. In medicine, this is the difference between a doctor who gives the right diagnosis by luck and one who follows sound clinical reasoning to get there.

This technique is used several ways:

- **Model development:** AI labs use LLM judges to quickly evaluate experimental models during training.
- **Quality monitoring:** Companies deploying LLMs use judges to continuously monitor response quality in production — flagging responses below standards.
- **Comparing models:** Organizations set up automated "tournament" evaluations where an LLM judge compares responses from different models side by side.

> **Simplification Note:** Using one AI to evaluate another creates obvious concerns about bias — what if the judge has the same weaknesses as the model being evaluated? Best practice is to use a different, stronger model as judge, and to validate LLM judge scores against human evaluations periodically. "LLM as a Judge" is increasingly used not just for evaluating models but for evaluating AI agent workflows — assessing whether a multi-step task was completed correctly, which is harder to test with traditional benchmarks.

---

## Why This Matters for Your Organization

Understanding evaluation is where you stop being a passive buyer and start being a strategic one. Over 80% of AI investments produce no meaningful EBIT impact — and poor evaluation is a major reason:

- **Benchmarks help you shortlist, not decide.** Public benchmarks tell you which models are in the top tier generally. They don't tell you which model is best for *your* use case. Demand proof on your terms, not theirs.

- **You need YOUR benchmarks.** Generic benchmarks measure generic capabilities. You need to know: can this model answer *your* customers' questions correctly? Does it follow *your* sales methodology? Does it understand *your* product terminology? Building evaluation questions specific to your organization is one of the highest-ROI investments in AI — not accuracy metrics, but actual professional quality scores judged against the standards your best people set. Think BankerToolBench, but for your domain.

- **LLM-as-a-Judge enables continuous quality monitoring.** You can't have a human review every response once you deploy. An LLM judge monitors quality at scale, alerting you when responses drift below standards — like a chief medical officer reviewing charts.

- **Institutional knowledge shapes what "good" means.** A generically helpful response might not be a good response for *your* organization. Evaluation criteria grounded in your values, terminology, and processes ensure the AI represents you correctly.

The organizations getting the most value from AI aren't using the highest-scoring models on public benchmarks. They're the ones who defined what "good" looks like in their specific context — and continuously measure against it. Your evaluation framework is your quality moat.

---

## Key Takeaway

Evaluation data tests what a model actually learned (not what it memorized); benchmarks provide standardized comparison across models (like board exams for doctors); and LLM-as-a-Judge enables scalable quality assessment using AI to evaluate AI — but the most important evaluations are the ones grounded in your organization's specific definition of "good."

---

*Previous: [Residency — Learning from Mentors](03-residency.md)* | *Next: [Clinical Reasoning — How LLMs Think](05-clinical-reasoning.md)* | *Back to [Series Overview](00-overview-the-journey.md)*
