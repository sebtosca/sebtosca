# Sebastien Toscano

**AI Engineer** · Paris, France · Open to remote

---

## About

AI Engineer with a Master's in Artificial Intelligence from SKEMA Business 
School and ESIEA School of Engineering (2025), with graduate research in 
Automated Machine Learning. I specialize in building and shipping AI systems 
end-to-end — from retrieval pipelines and LLM APIs to production infrastructure, 
monitoring, and automated evaluation. My current focus is agentic system design: 
building autonomous AI workflows with observability, tool use, and orchestration 
patterns that hold up under real operating conditions.

---

## Projects

### [Cortex — Financial Intelligence Retrieval Platform](https://github.com/sebtosca/Cortex-Production-Grade-Retrieval-and-Intelligence-Platform)

Production-grade RAG platform built to demonstrate full AI systems engineering 
depth: hybrid vector retrieval, async ingestion, distributed tracing, and 
automated quality evaluation with a custom domain-specific metric.

**Core finding:** hybrid retrieval + cross-encoder reranking at k=5 delivers 
the same recall as k=20 at 40% of the latency cost. Capping the reranker at 
k=5 reclaimed ~150ms per request — enough headroom to run a second-pass Claude 
Sonnet verification on answers that score below the `financial_groundedness` 
threshold.

**Stack:** Claude Haiku 4.5 · bge-m3 · Qdrant (RRF hybrid search) · 
CrossEncoder reranker · FastAPI + SSE · ARQ/Redis async ingestion · 
PostgreSQL · OpenTelemetry → Jaeger · RAGAS + custom eval metric · 
GitHub Actions CI quality gate

**Retrieval benchmark (gold set):**

| Strategy | Avg latency | Recall@5 |
|---|---|---|
| Dense only | 43ms | 0.712 |
| Sparse only | 37ms | 0.684 |
| Hybrid (RRF) | 52ms | 0.748 |
| **Hybrid + rerank (k=5)** | **248ms** | **0.876** |

**Evaluation (Claude Sonnet 4.6 as judge):**

| Metric | Score | Threshold |
|---|---|---|
| Faithfulness | 0.875 | ≥ 0.70 |
| Answer relevancy | 0.912 | ≥ 0.60 |
| Context recall | 0.730 | ≥ 0.65 |
| Financial groundedness | 0.900 | ≥ 0.80 |

`financial_groundedness` is a custom metric: Claude Sonnet reviews each answer 
against its retrieved passages and flags financial claims absent from or not 
inferable from the context — targeting the hallucination failure mode specific 
to financial documents.

---

### [Toxic Comment Classification](https://github.com/sebtosca/toxic-comment-classification)

Multi-label toxicity classifier with adversarial robustness evaluation. 
Fine-tuned RoBERTa + LightGBM ensemble with explicit hardening against 
text obfuscation attacks (backtranslation, synonym substitution, dynamic 
threshold adjustment).

**Stack:** PyTorch · RoBERTa · LightGBM · Scikit-learn · BERT embeddings

**Results (fine-tuned RoBERTa):** F1 Macro 0.459 · ROC-AUC Macro 0.797 on 
obfuscated test set — the harder evaluation target, not the clean baseline.

---

## Stack

**AI / LLM**
Python · PyTorch · LangChain · LangGraph · LiteLLM · Claude API · 
Hugging Face (bge-m3, RoBERTa, cross-encoders) · RAGAS

**Retrieval / Evaluation**
Qdrant · hybrid search (RRF) · cross-encoder reranking · 
OpenTelemetry · Jaeger · custom eval metrics

**Infra / Backend**
FastAPI · Docker · Redis · PostgreSQL · ARQ · AWS · GCP · Scikit-learn

---

## Currently

**Building:** agentic systems with production-grade observability — tool 
calling, orchestration, escalation handling, traceability across centralized 
and decentralized agent topologies.

**Learning:** production agentic system design · system design fundamentals 
for AI infrastructure at scale.

---

*Open to AI Engineer roles · Paris, France · Remote*
