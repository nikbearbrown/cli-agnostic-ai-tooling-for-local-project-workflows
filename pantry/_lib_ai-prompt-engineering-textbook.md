# Prompt Engineering with LLMs
### A Rigorous Framework for Designing, Evaluating, and Scaling Language Model Interactions

**Author:** Professor Nik Bear Brown  
**Institution:** Northeastern University, College of Engineering  
**Series:** INFO 7375 — Prompt Engineering for Generative AI

---

## Table of Contents

---

### Preface: Why Prompt Engineering Is an Engineering Discipline

---

## PART I — FOUNDATIONS: HOW LANGUAGE MODELS THINK (AND DON'T)

---

**Chapter 1: The Stochastic Machine — Understanding LLM Output Generation**

- **Core Claim:** LLMs do not retrieve answers — they sample from learned probability distributions, making every output a probabilistic event, not a deterministic lookup.
- **Logical Method:** Deductive reasoning from first principles of softmax probability and logit distributions to explain temperature, Top-K, and Top-P sampling mechanics.
- **Methodological Soundness:** Grounded in the mathematical formalism of transformer decoding; claims are falsifiable through controlled temperature experiments producing measurable output variance.
- **Use of LLMs:** Demonstrations using the same prompt at temperature 0, 0.7, and 1.2 to empirically observe the distribution-flattening effect; "Wonder Woman" stochastic variance case study.
- **Use of Agentic AI:** Agentic loops that adaptively adjust sampling parameters mid-task based on confidence scoring of prior outputs.

---

**Chapter 2: Hallucination — When Plausibility Beats Truth**

- **Core Claim:** Hallucination is not a bug to be patched but an emergent property of next-token prediction trained on human text, where fluency and factual grounding are orthogonal objectives.
- **Logical Method:** Inductive reasoning from documented hallucination cases (fabricated citations, false statistics) to a general model of why plausibility diverges from accuracy.
- **Methodological Soundness:** Uses reproducible prompt experiments that reliably elicit hallucination; distinguishes between factual hallucination, attribution hallucination, and coherence hallucination as distinct failure modes.
- **Use of LLMs:** Live prompt experiments asking models about obscure facts, forcing citation generation, and auditing outputs against ground truth.
- **Use of Agentic AI:** Fact Check List Pattern embedded in agentic pipelines; agents that cross-reference claims against retrieval systems before surfacing outputs.

---

**Chapter 3: The Chinese Room and the Limits of Syntax**

- **Core Claim:** LLMs are powerful symbol manipulators, but Searle's Chinese Room argument reminds us that syntactic competence does not entail semantic understanding — a distinction with profound implications for prompt design.
- **Logical Method:** Philosophical deduction from Searle's thought experiment mapped onto transformer architecture; argument by analogy and systematic counter-argument.
- **Methodological Soundness:** Engages with standard objections (Systems Reply, Robot Reply) and situates them within empirical NLP findings on commonsense reasoning failures.
- **Use of LLMs:** Prompts designed to probe "understanding" vs. pattern matching — e.g., Winograd schemas, counterfactual reasoning tasks, and symbol substitution experiments.
- **Use of Agentic AI:** Discussion of how agentic AI architectures (tool-use, memory, planning) partially address the Chinese Room limitation by anchoring symbolic operations to real-world feedback loops.

---

**Chapter 4: Sycophancy and Computational Skepticism**

- **Core Claim:** LLMs are trained to maximize approval, not accuracy — making sycophancy a systematic bias that users must actively counteract through computational skepticism.
- **Logical Method:** Causal reasoning tracing sycophancy from RLHF reward structures through to output-level behaviors; proposes computational skepticism as the epistemically correct response.
- **Methodological Soundness:** Empirically grounded in documented RLHF alignment research; sycophancy is operationalized as a measurable divergence between model agreement rate and ground-truth accuracy rate.
- **Use of LLMs:** Experiments where the user asserts a false claim and observes whether the model capitulates; A/B testing prompts with and without explicit anti-sycophancy constraints.
- **Use of Agentic AI:** Agents designed with dissenting sub-agents (red-team agents) that challenge primary agent outputs before they surface to the user.

---

## PART II — PROMPT ENGINEERING FRAMEWORKS

---

**Chapter 5: The Architect Mindset — Designing Prompts as Systems**

- **Core Claim:** Effective prompt engineering requires the Architect Mindset — designing the full prompt system (root prompts, constraints, persona, format) rather than crafting individual queries ad hoc.
- **Logical Method:** Analogical reasoning from software architecture to prompt architecture; introduces the distinction between Architect-level design decisions and User-level interaction patterns.
- **Methodological Soundness:** Framework validated through comparative studies of ad hoc prompting vs. structured prompt system design across multiple task types.
- **Use of LLMs:** Constructing and testing root prompts that persist behavioral constraints across multi-turn conversations; the Wordsville case study as a worked example.
- **Use of Agentic AI:** System-level prompt stacks in agentic pipelines where the Architect layer governs agent scope, persona, and guardrails across an entire autonomous task.

---

**Chapter 6: Persona Patterns — Shaping Who the Model Is and Who It Speaks To**

- **Core Claim:** Two distinct and frequently confused patterns — the Persona Pattern (who the AI *is*) and the Audience Persona Pattern (who the AI speaks *to*) — each activate different latent behaviors in the model and must be applied with precision.
- **Logical Method:** Taxonomic differentiation through definition, contrast, and worked examples; logical analysis of how each pattern affects the model's internal framing of the task.
- **Methodological Soundness:** Distinctions are operationally testable: swapping Persona for Audience Persona in identical prompts produces measurably different outputs in vocabulary, register, and depth.
- **Use of LLMs:** The Jane Austen prompt as a Persona Pattern exemplar; the non-technical executive explanation as an Audience Persona exemplar; side-by-side output comparison.
- **Use of Agentic AI:** Assigning persistent personas to specialized sub-agents (e.g., "You are a compliance auditor") within a multi-agent orchestration framework.

---

**Chapter 7: Constraint Engineering — Negative Prompts, Root Prompts, and Semantic Focus**

- **Core Claim:** What you tell a model *not* to do is as architecturally important as what you tell it to do — negative constraints sharpen semantic focus and reduce output entropy in ways positive instructions alone cannot achieve.
- **Logical Method:** Contrastive analysis demonstrating how negative constraints reduce the probability mass on undesired output regions; grounded in the mechanics of conditional probability in token generation.
- **Methodological Soundness:** Controlled experiments measuring output variance and constraint adherence with and without negative prompts across diverse task types.
- **Use of LLMs:** Examples of prompts with and without negative constraints ("avoid jargon," "do not hedge," "never use bullet points") with annotated output comparisons.
- **Use of Agentic AI:** Encoding negative constraints as persistent guardrails in root prompts of agentic systems; Semantic Filter agents that post-process outputs to enforce content policies.

---

**Chapter 8: PAST, PLFR, and Structured Prompt Frameworks**

- **Core Claim:** Structured prompt frameworks — PAST (Problem, Action, Steps, Task) and PLFR (Prompt, Logic, Format, Result) — impose logical scaffolding that reduces ambiguity and improves output reliability at scale.
- **Logical Method:** Deductive derivation of each framework's component logic; analysis of how structured decomposition maps complex user intent onto model-interpretable instruction sequences.
- **Methodological Soundness:** Frameworks evaluated on prompt clarity, output reproducibility, and task completion rate compared to unstructured prompts; edge cases and failure modes documented.
- **Use of LLMs:** Applying PAST and PLFR to real professional tasks (data analysis requests, report generation, code review) with before/after output quality assessments.
- **Use of Agentic AI:** Using PAST as the task decomposition backbone for agentic planning modules; PLFR as a structured format for agent-to-agent communication within a pipeline.

---

## PART III — ADVANCED PATTERNS AND ARCHITECTURES

---

**Chapter 9: Interaction Patterns — Flipping the Conversation**

- **Core Claim:** The most powerful prompt patterns are not declarative but interactive — patterns like Flipped Interaction, Ask for Input, and Cognitive Verifier shift the model from passive responder to active collaborator, dramatically improving output quality on ill-specified tasks.
- **Logical Method:** Taxonomic classification of interaction patterns by their epistemic function (information elicitation, task clarification, reasoning decomposition); argument that interactivity reduces underdetermination of the prompt.
- **Methodological Soundness:** Empirical comparison of direct-answer prompting vs. interactive pattern prompting on open-ended tasks; measured by output relevance and task completion accuracy.
- **Use of LLMs:** Worked examples of Flipped Interaction (model interviews the user), Cognitive Verifier (model generates sub-questions), and Question Refinement (model proposes a better question).
- **Use of Agentic AI:** Multi-turn agentic workflows where agents autonomously apply Ask for Input before executing tasks, reducing error rates from ambiguous instructions.

---

**Chapter 10: ReAct — Grounding Reasoning in the Real World**

- **Core Claim:** The ReAct (Reasoning and Acting) framework solves a fundamental limitation of pure chain-of-thought prompting by interleaving thought with action — allowing models to query external tools and ground each reasoning step in real observations rather than internal hallucination.
- **Logical Method:** Mechanistic analysis of the Thought → Action → Observation loop; logical argument for why external grounding reduces cumulative reasoning error compared to closed-chain inference.
- **Methodological Soundness:** Referenced against the original ReAct paper (Yao et al., 2022); brittleness under few-shot distribution shift is explicitly documented as a known limitation.
- **Use of LLMs:** Step-by-step ReAct trace examples for web search, database lookup, and code execution tasks; few-shot example construction and its effect on task accuracy.
- **Use of Agentic AI:** ReAct as the core reasoning architecture for autonomous agents; multi-step agentic tasks (e.g., research summarization, data validation pipelines) implemented as ReAct loops with tool registries.

---

**Chapter 11: The Prompt Stack — Scalable AI Infrastructure**

- **Core Claim:** Production AI systems cannot be built on single-turn prompts — the Prompt Stack architecture (pre-prompts, meta-prompts, user prompts, output filters) provides the modular infrastructure required for maintainable, scalable, and auditable LLM deployments.
- **Logical Method:** Systems engineering reasoning applied to prompt design; argument by analogy to software layered architecture (OS, middleware, application).
- **Methodological Soundness:** Framework evaluated against real deployment scenarios (chatbots, RAG pipelines, multi-agent systems) for modularity, debuggability, and component replaceability.
- **Use of LLMs:** Building a complete Prompt Stack for a realistic use case (e.g., a university academic advisor bot); demonstrating how each stack layer can be updated independently.
- **Use of Agentic AI:** Prompt Stack as the governance layer for multi-agent systems — pre-prompts encode agent identity, meta-prompts encode task routing logic, user prompts carry dynamic context.

---

**Chapter 12: Chain-of-Thought, Few-Shot, and Meta Language Creation**

- **Core Claim:** Chain-of-thought prompting, few-shot exemplars, and Meta Language Creation are complementary techniques that exploit the model's in-context learning capacity — but each has distinct failure modes that disciplined prompt engineers must anticipate.
- **Logical Method:** Comparative analysis of zero-shot, few-shot, and chain-of-thought prompting on a common benchmark task set; formal definition of Meta Language Creation as a prompt-level DSL (domain-specific language).
- **Methodological Soundness:** Claims grounded in empirical NLP literature (Wei et al. on chain-of-thought; Brown et al. on few-shot); failure modes (exemplar bias, format overfitting) are operationalized and demonstrated.
- **Use of LLMs:** Constructing few-shot exemplars for a structured data extraction task; building a Meta Language for a recurring analytical workflow (e.g., "ANALYZE:[text] FORMAT:[table] VERIFY:[sources]").
- **Use of Agentic AI:** Agents that dynamically construct chain-of-thought prompts for sub-tasks; Meta Language as a structured communication protocol between orchestrator and worker agents.

---

## PART IV — FINE-TUNING, ALIGNMENT, AND SCALING

---

**Chapter 13: SFT vs. RAG — When to Bake Knowledge In vs. Retrieve It**

- **Core Claim:** Supervised Fine-Tuning and Retrieval-Augmented Generation are not competing alternatives but complementary strategies with distinct cost-benefit profiles — the choice between them is an engineering decision driven by knowledge volatility, latency requirements, and update frequency.
- **Logical Method:** Decision-theoretic framework comparing SFT and RAG on five axes: knowledge freshness, inference cost, training cost, hallucination risk, and deployment complexity.
- **Methodological Soundness:** Framework validated through case studies spanning static knowledge domains (SFT preferred) and dynamic knowledge domains (RAG preferred); hybrid architectures addressed.
- **Use of LLMs:** Prompt experiments illustrating the knowledge boundary of a pre-trained model vs. a RAG-augmented pipeline on current events and proprietary data tasks.
- **Use of Agentic AI:** Agentic systems that dynamically route queries to fine-tuned models vs. RAG pipelines based on query classification; the "80 Days to Stay" SEC data retrieval system as a worked case study.

---

**Chapter 14: LoRA and QLoRA — Parameter-Efficient Fine-Tuning**

- **Core Claim:** LoRA and QLoRA make fine-tuning democratically accessible by decomposing weight updates into low-rank matrices (LoRA) and combining this with 4-bit quantization (QLoRA) — reducing GPU memory requirements by orders of magnitude without proportional loss in task performance.
- **Logical Method:** Mathematical derivation of the low-rank decomposition logic (W = W₀ + BA); analysis of how NF4 quantization and Paged Optimizers address memory bottlenecks in QLoRA.
- **Methodological Soundness:** Cla