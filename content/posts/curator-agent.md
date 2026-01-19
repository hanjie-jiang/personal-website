---
title: "The Curator Agent: Bridging the Gap Between SOTA Research and Engineering Reality"
date: 2026-01-19
draft: false
tags: ["AI Agents", "LLM", "Databricks", "Qwen", "System Architecture", "MLOps"]
categories: ["Machine Learning", "AI Agents"]
description: "A modular, resource-efficient Level 1 Agent designed to autonomously track, score, and deduplicate daily AI research papers using deterministic cognitive pipelines."
---

## The Challenge: The "Hugging Face Daily Papers" Signal-to-Noise Ratio

In the rapidly evolving AI landscape, staying updated with SOTA (State-of-the-Art) research is a double-edged sword. Every morning, dozens of papers are released. For a Lead ML Scientist, the manual task of filtering these takes hours, leading to "recommendation system cocoons" or information overload.

## The Solution: A Modular Cognitive Agent

Unlike a linear script, **The Curator Agent** was built as a Level 1 Agent—a deterministic cognitive pipeline. It doesn't just "scrape" data; it perceives, thinks, and remembers.

### Core Architecture

The system is built on the principle of **High Cohesion and Low Coupling**, comprising three distinct modules:

1. **PerceptionTools (The Eyes):** Robust API ingestion logic that bypasses fragile DOM parsing. It monitors the Hugging Face daily paper feeds with an SLA-focused mindset.

2. **CognitiveBrain (The Logic Engine):** Powered by **Qwen-2.5-14B** (running on Databricks Graviton CPU clusters).
   - **Scientist Mode:** Performs absolute quality scoring (Novelty, Results, Completeness).
   - **Critic Mode:** Validates relative novelty to prevent redundant "incremental work" from cluttering the feed.

3. **PaperArchive (The Memory):** A vector-based long-term memory that handles semantic deduplication, ensuring that if you've seen a similar architecture yesterday, you won't waste time on it today.

---

## Technical Deep Dive: "Technical Empathy" in Design

As a Lead Scientist, I built this with **Unit Economics** and **Engineering Constraints** in mind:

### Circuit Breaker Logic
If the "Scientist" scores a paper below 7/10, the pipeline immediately kills the process for that candidate, saving inference costs and latency.

### Graviton Optimization
Instead of demanding expensive GPUs, the Brain is optimized for ARM64/CPU architectures (bfloat16 precision), proving that "Agentic" doesn't have to mean "Expensive."

**Key Configuration:**
```python
# CPU-optimized inference
dtype = "bfloat16"  # ARM64 native support
max_tokens = 2000
temperature = 0.1   # Deterministic outputs
```

### Pydantic Guardrails
All model outputs are strictly validated via Pydantic schemas, transforming probabilistic LLM chatter into deterministic system data.

**Example Schema:**
```python
class ScientistScore(BaseModel):
    novelty: int = Field(ge=1, le=10)
    results: int = Field(ge=1, le=10)
    completeness: int = Field(ge=1, le=10)
    overall_score: int = Field(ge=1, le=10)
    reasoning: str
```

---

## Impact

### Efficiency Gains
- **Reduced a 2-hour manual research morning into a 3-minute high-fidelity automated brief**
- CPU-only inference: ~30-60 seconds per paper (on ARM64 Graviton)
- Cost: <$0.01 per paper analyzed

### Autonomy
The first step in my journey toward building fully autonomous workspace agents that change how humans interact with complex information.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                   ResearchLab (Orchestrator)             │
└───────┬─────────────────────────┬─────────────┬─────────┘
        │                         │             │
        ▼                         ▼             ▼
┌───────────────┐        ┌────────────────┐  ┌──────────────┐
│ PerceptionTools│       │ CognitiveBrain │  │ PaperArchive │
│  (API Fetch)   │       │  Qwen-2.5-14B  │  │   (Vectors)  │
└───────────────┘        └────────────────┘  └──────────────┘
        │                         │                    │
        │   Fetch Papers          │  Score & Evaluate  │  Deduplicate
        ▼                         ▼                    ▼
    HuggingFace              Circuit Breaker       Semantic Search
     Daily Feed               (Score < 7)          (Similarity)
```

---

## Technical Stack

- **Model:** Qwen-2.5-14B-Instruct (bfloat16)
- **Infrastructure:** Databricks (AWS Graviton / ARM64 CPU)
- **Orchestration:** Custom Python pipeline with Pydantic validation
- **Memory:** SentenceTransformers for vector embeddings
- **Guardrails:** Structured output via Pydantic schemas

---

## Key Learnings

1. **Agentic AI ≠ Expensive:** CPU-optimized LLMs can deliver production-grade performance without GPU costs
2. **Deterministic Outputs Matter:** Pydantic schemas transform unreliable LLM outputs into reliable system data
3. **Engineering Empathy:** Every architectural decision should consider unit economics (cost vs. value)
4. **Circuit Breakers Save Money:** Early termination logic prevents wasted inference on low-quality candidates

---

## What's Next: Level 3 Agents

This Level 1 (Deterministic Pipeline) agent sets the foundation for **Level 3 Autonomous Agents** using:
- **LangGraph:** For complex multi-step reasoning
- **ReAct Patterns:** For tool-using autonomous agents
- **Dynamic Planning:** Adapting to changing research landscapes

---

> "The best AI products aren't just wrappers; they are systems that understand the cost of a hallucination and the value of an engineer's time."

---

## Footnotes

This project demonstrates that thoughtful system design can deliver AI value without excessive infrastructure costs. By optimizing for CPU architectures and implementing strict guardrails, we prove that **Agentic AI can be both powerful and economical**.

Stay tuned for the Level 3 evolution.
