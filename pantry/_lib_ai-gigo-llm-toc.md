# GIGO - A Crash Course in Data with LLMs
*By Megha Patel and Nik Bear Brown*

---

## Table of Contents

---

### Chapter 1: The GIGO Imperative — Why Data Quality Is the Foundation of AI

**Core Claim:** All downstream AI outputs — including those from LLMs — inherit the structural flaws of their input data; computational skepticism is the only reliable defense.

**Logical Method:** Deductive reasoning from first principles; the GIGO axiom applied to the full AI pipeline.

**Methodological Soundness:** Grounded in decades of computing theory and validated by modern LLM failure modes (hallucination, bias, drift).

**Use of LLMs:** LLMs are introduced as the latest and most complex instance of GIGO risk — their scale amplifies both data garbage and its consequences.

**Use of Agentic AI:** Introduction to agentic auditors as automated GIGO sentinels capable of flagging data quality issues without human intervention.

**Case Study:** GPT-4 hallucinating legal citations — tracing the garbage back to its source in pretraining corpora.

---

### Chapter 2: Understanding Data — Types, Structures, and the Taxonomy of "Garbage"

**Core Claim:** Garbage is not uniform; its type (missing, mislabeled, imbalanced, drifted) determines which remediation strategy is appropriate.

**Logical Method:** Taxonomic classification — categorical, numerical, temporal, spatial, multimedia, and text data types mapped to their failure modes.

**Methodological Soundness:** Draws on established data science ontologies; failure modes validated against real-world pipeline case studies.

**Use of LLMs:** LLMs used as data type classifiers and schema validators to automatically detect when data is in the wrong format or category.

**Use of Agentic AI:** Agents that continuously audit incoming data streams against a known schema, flagging type mismatches in real time.

**Case Study:** Electronic health records with mixed categorical/numeric fields causing downstream model failure in a clinical NLP pipeline.

---

### Chapter 3: Data Quality Assessment — Validity, Accuracy, Completeness, and Timeliness

**Core Claim:** Data quality is multi-dimensional; a dataset can be accurate yet untimely, or complete yet invalid — each dimension requires its own diagnostic.

**Logical Method:** Multi-criteria evaluation framework; each quality dimension is assessed independently before synthesis.

**Methodological Soundness:** Aligned with ISO/IEC 25012 data quality standards and DAMA-DMBOK framework.

**Use of LLMs:** LLMs prompted with quality rubrics to perform automated quality audits on documentation, metadata, and semi-structured text fields.

**Use of Agentic AI:** Agents cross-reference incoming records against authoritative external sources (APIs, knowledge bases) to verify timeliness and accuracy.

**Case Study:** COVID-19 case data reporting inconsistencies across jurisdictions — a real-world multi-dimensional quality failure.

---

### Chapter 4: Handling Missing Data — From MCAR to MNAR and Everything Between

**Core Claim:** The mechanism behind missingness — not just its presence — determines whether imputation helps or harms the model.

**Logical Method:** Conditional reasoning: MCAR → deletion acceptable; MAR → model-based imputation; MNAR → structural modeling required.

**Methodological Soundness:** Rubin's (1976) missingness taxonomy; validated through empirical comparison of imputation strategies on benchmark datasets.

**Use of LLMs:** LLMs used to generate natural language explanations of why missingness may be occurring (e.g., parsing survey notes to infer MNAR mechanisms).

**Use of Agentic AI:** MICE and KNN imputation agents that select the appropriate strategy based on detected missingness pattern, then validate imputation quality through distribution comparison.

**Case Study:** Clinical trial dropout data — imputing missing patient outcomes without biasing efficacy estimates.

---

### Chapter 5: Data Cleaning — Removing Duplicates, Errors, and Structural Noise

**Core Claim:** Structural errors — typos, inconsistent capitalization, duplicate records — are silent model killers that compound at scale.

**Logical Method:** Rule-based and algorithmic cleaning pipelines; Levenshtein distance, hashing, regex, and fuzzy matching for structural repair.

**Methodological Soundness:** Each cleaning step is benchmarked against before/after model performance metrics.

**Use of LLMs:** LLMs used for intelligent deduplication — identifying records that describe the same entity using semantic similarity rather than exact string matching.

**Use of Agentic AI:** Agents that run continuous deduplication and structural validation on data lakes, logging all changes for lineage tracking.

**Case Study:** Customer master data management at a retail company — merging millions of duplicate customer records using LLM-powered entity resolution.

---

### Chapter 6: Data Transformation — Normalization, Scaling, and Feature Engineering

**Core Claim:** Poorly scaled or untransformed features are a form of garbage that silently distorts distance-based and gradient-based models.

**Logical Method:** Mathematical derivation of normalization techniques (Min-Max, Z-score, Robust Scaling) with proof of their effect on model geometry.

**Methodological Soundness:** Empirical validation across SVM, KNN, and neural network benchmarks showing performance sensitivity to scaling choices.

**Use of LLMs:** LLMs recommend appropriate scaling strategies based on natural language descriptions of the data and the chosen model family.

**Use of Agentic AI:** Feature engineering agents that automatically generate, test, and rank new features, selecting those that reduce model error without introducing leakage.

**Case Study:** Fraud detection in financial transactions — the outsized impact of log-scaling skewed transaction amounts on model AUC.

---

### Chapter 7: Data Bias — Detecting and Mitigating Systematic Distortions

**Core Claim:** Bias is not just a social concern — it is a technical failure mode that produces systematically incorrect predictions for subpopulations.

**Logical Method:** Operationalizing bias types (selection, confirmation, historical, implicit) as statistical divergences between subgroup distributions.

**Methodological Soundness:** Grounded in fairness literature (demographic parity, equalized odds); validated through disparity analysis across protected attributes.

**Use of LLMs:** LLMs audited for embedded biases via counterfactual prompting — substituting demographic attributes and measuring output variance.

**Use of Agentic AI:** Fairness agents that continuously monitor model predictions for disparate impact and trigger retraining when thresholds are breached.

**Case Study:** Hiring algorithm bias at a major tech company — using SHAP analysis and stratification to detect and remediate gender-correlated feature proxies.

---

### Chapter 8: Sampling Theory and the Garbage of Non-Representative Data

**Core Claim:** A perfectly clean dataset sampled from the wrong population produces perfectly wrong models — representativeness is a prerequisite for validity.

**Logical Method:** Statistical sampling theory (SRS, stratified, cluster, systematic); Central Limit Theorem as the mathematical backbone of inference.

**Methodological Soundness:** Theoretical grounding in Neyman-Pearson sampling theory; empirically illustrated through bootstrap confidence intervals.

**Use of LLMs:** LLMs used to synthesize stratification plans from natural language descriptions of target populations and research objectives.

**Use of Agentic AI:** Sampling agents that dynamically adjust oversampling and undersampling ratios during training based on live performance feedback.

**Case Study:** Polling failure in the 2016 U.S. election — a masterclass in sampling frame error and its consequences.

---

### Chapter 9: Data Integration — Combining Sources Without Combining Their Flaws

**Core Claim:** Data integration multiplies garbage if provenance is not tracked — each merge is an opportunity to inherit another system's errors.

**Logical Method:** Entity resolution, schema matching, and semantic harmonization as the three layers of integration quality control.

**Methodological Soundness:** Validated through ETL pipeline audits; lineage tracking via Apache Atlas used as ground truth.

**Use of LLMs:** LLMs used for semantic schema matching — identifying equivalent fields across heterogeneous data sources using natural language understanding.

**Use of Agentic AI:** Integration agents orchestrated via Apache Airflow DAGs that validate data at each merge point and halt pipelines on quality failures.

**Case Study:** Merging hospital EHR systems after a healthcare system acquisition — resolving conflicting patient identifiers and diagnostic code schemas.

---

### Chapter 10: Data Visualization — Making Garbage Visible

**Core Claim:** The right visualization reveals patterns of data corruption that are invisible to numerical summaries.

**Logical Method:** Application of Gestalt principles and visual design hierarchy to diagnostic visualization — choosing the chart type that makes the problem visible.

**Methodological Soundness:** Empirically grounded in pre-attentive processing theory; chart selection validated against detection accuracy benchmarks.

**Use of LLMs:** LLMs generate visualization code (Matplotlib, Plotly, D3.js) from natural language descriptions of the diagnostic question.

**Use of Agentic AI:** Visualization agents that automatically produce a diagnostic dashboard when a new dataset is ingested, flagging suspected anomalies visually.

**Case Study:** John Snow's cholera map — the original use of visualization to detect the "garbage" of a misattributed disease source.

---

### Chapter 11: Exploratory Data Analysis with LLMs — Computational Skepticism in Practice

**Core Claim:** EDA is not a preliminary step — it is a continuous act of computational skepticism that should be integrated throughout the modeling lifecycle.

**Logical Method:** Iterative hypothesis generation and falsification; Popperian falsifiability applied to data assumptions.

**Methodological Soundness:** Structured EDA protocols validated against model performance improvements on real-world datasets.

**Use of LLMs:** LLMs act as an interactive EDA partner — generating hypotheses, writing analysis code, and interpreting results in natural language.

**Use of Agentic AI:** EDA agents that autonomously explore a new dataset, generate a structured report of findings, and propose a cleaning roadmap.

**Case Study:** Discovering a data leakage issue in a Kaggle competition through LLM-assisted EDA before model submission.

---

### Chapter 12: Statistical Hypothesis Testing — Avoiding the Garbage of p-Hacking

**Core Claim:** Statistical tests are only as valid as the assumptions behind them — violating normality, independence, or homoscedasticity produces garbage p-values.

**Logical Method:** Formal hypothesis testing (null/alternative, Type I/II error, power analysis); Shapiro-Wilk, Anderson-Darling, and KS tests for assumption validation.

**Methodological Soundness:** Pre-registration of hypotheses and multiple comparisons correction (Bonferroni, FDR) as structural safeguards.

**Use of LLMs:** LLMs explain statistical test selection in plain language and warn users when their data violates test assumptions.

**Use of Agentic AI:** Hypothesis testing agents that automatically select the appropriate test, validate assumptions, run corrections for multiple comparisons, and flag p-hacking risk.

**Case Study:** The replication crisis in psychology — how p-hacking produced decades of garbage findings and how pre-registration is fixing it.

---

### Chapter 13: Imbalanced Data — Fixing the Representation Gap with SMOTE, GANs, and LLMs

**Core Claim:** Class imbalance is not a data problem to be ignored — it is a structural form of garbage that causes models to fail precisely when accuracy matters most.

**Logical Method:** Systematic comparison of oversampling (SMOTE, ADASYN), undersampling (Tomek Links), and generative approaches (CTGAN, TVAE).

**Methodological Soundness:** Validated using AUROC, G-Mean, and MCC metrics on benchmark imbalanced datasets (fraud, medical, fault prediction).

**Use of LLMs:** LLMs generate realistic synthetic minority-class text samples for NLP classification tasks.

**Use of Agentic AI:** Balancing agents that dynamically adjust class weights and synthetic sample generation rates during training based on live validation metrics.

**Case Study:** Credit card fraud detection — how SMOTE combined with XGBoost increased minority class recall from 34% to 91%.

---

### Chapter 14: Feature Selection and Dimensionality Reduction — Cutting Noise, Keeping Signal

**Core Claim:** High dimensionality is a form of structural garbage — irrelevant features add noise, increase computation, and mask the true predictive signal.

**Logical Method:** Filter, wrapper, and embedded feature selection methods; PCA and t-SNE for manifold-based dimensionality reduction.

**Methodological Soundness:** Feature importance validated through permutation testing and ablation studies; PCA eigenvalue analysis used to justify component selection.

**Use of LLMs:** LLMs used to generate feature hypotheses from domain knowledge, reducing the search space before automated selection.

**Use of Agentic AI:** Feature selection agents that run recursive elimination with cross-validation, report selected features with rationale, and monitor for feature drift over time.

**Case Study:** Genomics — reducing 20,000 gene expression features to 50 predictive biomarkers for cancer subtype classification.

---

### Chapter 15: Data Encoding — Converting Categorical Garbage into Learnable Signal

**Core Claim:** Incorrect encoding of categorical variables is one of the most common and consequential forms of silent garbage in machine learning pipelines.

**Logical Method:** Systematic comparison of One-Hot, Ordinal, Target, Binary, and Count Encoding — matched to variable type and model architecture.

**Methodological Soundness:** Empirical benchmarking of encoding strategies against model performance on high-cardinality categorical datasets.

**Use of LLMs:** LLMs generate encoding recommendations and detect ordinal relationships in categorical variables through semantic analysis of category labels.

**Use of Agentic AI:** Encoding agents that auto-detect cardinality, detect ordering in categories using embedding similarity, and select the optimal encoding strategy.

**Case Study:** E-commerce recommendation — the performance gap between Label Encoding and Target Encoding for product category with 50,000 unique values.

---

### Chapter 16: Text Data — Pre-processing, Tokenization, and the Garbage of Unstructured Language

**Core Claim:** Raw text is among the noisiest data types — without systematic normalization, LLMs and NLP models learn the artifacts of human writing rather than its meaning.

**Logical Method:** Sequential pre-processing pipeline: contraction expansion → lowercasing → punctuation removal → stopword filtering → lemmatization/stemming.

**Methodological Soundness:** Ablation studies showing the contribution of each pre-processing step to downstream model accuracy.

**Use of LLMs:** LLMs used to perform context-aware text normalization — handling sarcasm, slang, and domain-specific abbreviations that rule-based systems miss.

**Use of Agentic AI:** Text pre-processing agents that apply different cleaning pipelines to different document types and languages, then validate output quality using embedding coherence metrics.

**Case Study:** Social media sentiment analysis — how emoji removal, slang normalization, and bot-account filtering changed model accuracy by 23%.

---

### Chapter 17: Multimedia Data — Cleaning Images, Audio, and Video for AI Pipelines

**Core Claim:** Multimedia garbage — noise, compression artifacts, label errors, and distribution shift — is harder to detect than tabular garbage but equally destructive to model performance.

**Logical Method:** Morphological operations for image cleaning; MFCC extraction and ZCR filtering for audio; frame-level quality scoring for video.

**Methodological Soundness:** Validated on benchmark medical imaging (MIMIC-CXR) and audio classification (UrbanSound8K) datasets.

**Use of LLMs:** Vision-language models (GPT-4V, LLaVA) used for automated image annotation quality auditing and anomaly detection.

**Use of Agentic AI:** Multimodal agents that process raw media, apply domain-appropriate cleaning, extract structured features, and flag low-quality samples for human review.

**Case Study:** Chest X-ray classification — how removing watermarks, normalizing exposure, and relabeling 3% of mislabeled images increased diagnostic model AUC by 0.08.

---

### Chapter 18: Spatial and Time-Series Data — Detecting Drift, Peaks, and Temporal Garbage

**Core Claim:** Temporal and spatial data carry a unique form of garbage — the context-dependent error that only appears when the ordering or location of data is respected.

**Logical Method:** ARIMA for stationarity testing and trend decomposition; CUSUM and Bayesian change point detection for drift identification; IQR-based peak detection.

**Methodological Soundness:** Validated against benchmark forecasting competitions (M4, M5) and sensor anomaly detection datasets.

**Use of LLMs:** LLMs interpret anomaly reports from time-series agents, generating natural language summaries of detected drift events for non-technical stakeholders.

**Use of Agentic AI:** Forecasting agents built with Greykite and fbProphet that autonomously detect seasonality, holiday effects, and concept drift, retraining models when drift thresholds are exceeded.

**Case Study:** Predictive maintenance in manufacturing — using temporal GIGO detection to reduce false alarms in turbine sensor data by 67%.

---

### Chapter 19: Data Drift and Pipeline Monitoring — Keeping Clean Data Clean

**Core Claim:** Data quality is not a one-time achievement — without continuous monitoring, clean pipelines degrade silently and at scale.

**Logical Method:** Statistical process control (SPC) applied to ML pipelines; Population Stability Index (PSI) and Kullback-Leibler divergence for drift quantification.

**Methodological Soundness:** Industry-validated monitoring frameworks (Evidently AI, WhyLogs, Arize) benchmarked against simulated drift scenarios.

**Use of LLMs:** LLMs generate incident reports and root cause analyses when monitoring agents detect anomalies in production pipelines.

**Use of Agentic AI:** Monitoring agents that run 24/7, compute drift metrics on incoming data, compare against baseline distributions, and trigger automated remediation or human escalation.

**Case Study:** Recommendation system degradation at a streaming platform — detecting and remediating covariate shift introduced by a UI change that altered user behavior.

---

### Chapter 20: Prompt Engineering — Preventing Garbage-In at the LLM Interface

**Core Claim:** For LLM-based systems, the prompt is the data — a poorly constructed prompt is the most direct path to garbage output.

**Logical Method:** Pattern-based prompt engineering — Persona, Chain-of-Thought, Cognitive Verifier, Flipped Interaction, and ReAct patterns mapped to specific GIGO failure modes.

**Methodological Soundness:** Validated through systematic A/B testing of prompt variants on factual accuracy, consistency, and task completion benchmarks.

**Use of LLMs:** Meta-application — LLMs used to generate, evaluate, and iterate on prompt designs for other LLM tasks.

**Use of Agentic AI:** Prompt optimization agents that automatically test prompt variants, score outputs against quality rubrics, and select the optimal prompt for production deployment.

**Case Study:** Legal document analysis — how switching from a zero-shot prompt to a Persona + Chain-of-Thought + Cognitive Verifier composite pattern reduced hallucination rate from 18% to 2%.

---

### Chapter 21: Agentic AI Architecture — Building Systems That Fix Their Own Garbage

**Core Claim:** The ultimate GIGO defense is a self-correcting pipeline — agentic AI systems that detect, diagnose, and remediate data quality issues autonomously.

**Logical Method:** Multi-agent system design: orchestrator agents, specialist agents (imputation, scaling, validation, monitoring), and human-in-the-loop escalation protocols.

**Methodological Soundness:** Evaluated on end-to-end pipeline benchmarks measuring data quality KPIs before and after agentic intervention.

**Use of LLMs:** LLMs serve as the reasoning core of each agent — interpreting tool outputs, making decisions, and generating natural language reports.

**Use of Agentic AI:** Full agentic architecture using LangGraph, AutoGen, or CrewAI — coordinating specialized agents across ingestion, cleaning, validation, modeling, and monitoring.

**Case Study:** Humanitarians.AI "80 Days to Stay" project — an agentic pipeline scraping, cleaning, and validating SEC filings and government databases to help international students find visa-sponsoring employers.

---

### Chapter 22: Computational Skepticism and AI Fluency — The Human in the GIGO Loop

**Core Claim:** Technology alone cannot solve GIGO — it requires practitioners fluent in the Nine Pillars of AI Fluency who treat every model output as a hypothesis awaiting falsification.

**Logical Method:** The Popperian framework of falsifiability applied to AI systems; adversarial validation as the operationalization of skepticism.

**Methodological Soundness:** Validated through curriculum outcomes at Northeastern University's INFO 7390 and through Humanitarians.AI publication records.

**Use of LLMs:** LLMs as thinking partners — used to stress-test assumptions, generate counterarguments, and identify blind spots in data analyses.

**Use of Agentic AI:** The "Popper Agent" — an adversarial AI that is explicitly tasked with attempting to break or falsify the outputs of other agents in the pipeline.

**Case Study:** The B Wells accountability platform — applying computational skepticism and multi-agent contradiction detection to political data to identify logical inconsistencies and constitutional violations at scale.

---

*Appendix A: GIGO Diagnostic Checklist — A Practitioner's Reference*
*Appendix B: LLM Prompt Pattern Library for Data Science*
*Appendix C: Agentic AI Tool Stack Reference (LangChain, LangGraph, AutoGen, CrewAI)*
*Appendix D: Key Formulas and Statistical Reference Tables*
*Appendix E: Recommended Datasets for Hands-On Practice*
