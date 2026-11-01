# Generative AI & Agentic Systems Engineering Lab

[![CI](https://github.com/lowkey999-netizen/genai-course-work/actions/workflows/ci.yml/badge.svg)](https://github.com/lowkey999-netizen/genai-course-work/actions/workflows/ci.yml)
![Python 3.12](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)
![pytest](https://img.shields.io/badge/tested_with-pytest-0A9EDC?style=flat&logo=pytest&logoColor=white)

![Tech Stack](https://img.shields.io/badge/Tech_Stack-Python_•_LangChain_•_Pydantic_•_Jinja2_•_Pytest_•_uv_•_Ollama_•_Hugging_Face_•_Groq_•_Gemini_•_GitHub_Actions-24292e?style=flat)

> _Built while following Ajit Byru's GenAI / Agentic AI course._

An applied engineering repository exploring the mechanics of Large Language Models, high-dimensional vector spaces, provider routing, and working toward agentic workflows with automated CI testing and strict schema enforcement.

---

## System Architecture

```text
                    ╭──────────────────────╮
                    │  User Dialogue / Req │
                    ╰──────────┬───────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │       State & Memory Pipeline        │
            │   Sliding / Summary · Token Budget   │
            ╰──────────────────┬───────────────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │      Defensive Prompt Pipeline       │
            │  Jinja2 Escape · Delimiters · Policy │
            ╰──────────────────┬───────────────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │           Provider Router            │
            ╰───────┬──────────────────────┬───────╯
                    │ Cloud                │ Edge / Local
                    ▼                      ▼
            ╭───────────────╮      ╭───────────────╮
            │ Groq / Gemini │      │  Ollama / HF  │
            ╰───────┬───────╯      ╰───────┬───────╯
                    │                      │
                    ╰──────────┬───────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │     Reasoning & Guardrail Filter     │
            │    Strip <scratchpad> · Leak Scan    │
            ╰───────┬──────────────────────┬───────╯
                    │ Tool Call            │ Final Text
                    ▼                      ▼
            ╭───────────────╮      ╭───────────────╮
            │ Tool Engine   │      │ Pydantic /    │
            │ JSON Dispatch │──┐   │ Schema Check  │
            ╰───────────────╯  │   ╰───────┬───────╯
                               │           │ [Valid]
                               │           ▼
                               │   ╭────────────────────────╮
                               │   │  Deterministic Action  │
                               │   ╰────────────────────────╯
                               │               ▲
                               ▼               │
            ╭──────────────────────────────────┴───╮
            │     Agent State Loop (LangChain)     │
            │   Tool Output Re-injection & State   │
            ╰──────────────────────────────────────╯
```

---

## Showcase Applications

Canonical reference workflows from the course demonstrating code-owned execution sequences where language models handle unstructured parsing and intent extraction:

- **[Automated Insurance Claim Intake](showcase/a2_insurance/README.md) (`showcase/a2_insurance`):** Parses free-text vehicle damage claims into validated structured forms (`ClaimForm`), routing claims by severity to automated fast-track payout or human adjuster queues.
- **[Healthcare Clinic Booking Flow](showcase/a3_healthcare/README.md) (`showcase/a3_healthcare`):** Multi-step patient conversational intake featuring pre-model emergency safety guards, model-based intent routing, dynamic slot-filling, and deterministic appointment scheduling.

---

## Modules Overview

| Module                                           | Core Technical Focus                                                                                                                                                                  | Status      | Documentation                           |
| :----------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---------- | :-------------------------------------- |
| **Module 01: Foundations & The Model Landscape** | BPE tokenization, vector embeddings, dimensionality reduction (PCA/SVD), multi-provider routing, local quantization, and multimodal structured extraction                             | Completed   | [Explore Module 01](module01/README.md) |
| **Module 02: Prompt Engineering & Reasoning**    | Production prompt design, structural delimiters, Jinja2 templating, private scratchpads, versioned prompt libraries, LLM-as-a-judge evaluation, and multi-layer defensive red-teaming | Completed   | [Explore Module 02](module02/README.md) |
| **Module 03: LLM Applications**                  | Multi-turn conversational memory, sliding window & summarization eviction, JSON tool schema dispatch, and stateful agent orchestration with LangChain                                 | In Progress | [Explore Module 03](module03/README.md) |

---

## Core Engineering Takeaways

- **Module 01 (Foundations & The Model Landscape):** Pre-computing BPE token allocations and vector dimensions locally exposes hidden cost and latency trade-offs before making API calls. While hosted accelerators provide high throughput, local quantization (int4) and self-hosted models offer strict data residency when handling sensitive records. _(See detailed session benchmarks and visualizers in [Module 01](module01/README.md).)_
- **Module 02 (Prompt Engineering & Reasoning):** Strict structural boundaries (XML delimiters, escaped tags) and versioned prompt files prevent prompt injection and unlock caching for static policies. Thinking strategies like Chain-of-Thought are crucial for smaller local models (flipping edge-case accuracy from 0/5 to 5/5) but inflate token costs on native reasoning models. Sealing private thoughts in a `<scratchpad>` curtain stripped by application code, alongside a leak scanner and instruction hierarchy, eliminated adversarial breakouts across 16 attack vectors (0% exploit rate) while maintaining 100% classification accuracy. _(See prompt library, accuracy tables, eval harness, and defense benchmarks in [Module 02](module02/README.md).)_
- **Module 03 (LLM Applications):** Multi-turn chat histories scale token costs quadratically ($O(N^2)$) if left unmanaged. While a 6-turn sliding window trimmed final-turn token load by ~46%, it triggered deterministic amnesia on early references. Progressive summarization cut final-turn token consumption by ~28% but discarded fine-grained reference tokens without explicit entity guards, demonstrating why stateful tool calling and structured memory persistence are essential for multi-turn production agents. _(See session experiments and tool benchmarks in [Module 03](module03/README.md).)_

---

## Engineering Practices

- **Automated CI (GitHub Actions):** Every commit triggers an automated pipeline running offline unit and logic tests across mock fixtures, preventing schema regressions and logic bugs without incurring API token costs.
- **Fast, Deterministic Environments:** Managed with [`uv`](https://docs.astral.sh/uv/) for rapid virtual environment resolution and exact cross-platform dependency locking via `uv.lock`.
- **Dual-Branch Upstream Architecture:** Employs an isolated two-branch Git strategy (`main` for personal engineering and documentation, `upstream-sync` as an untouched mirror for pulling course curriculum updates).

---

## Quickstart

### Prerequisites

- Python 3.12+
- [`uv`](https://docs.astral.sh/uv/) installed

### 1. Clone & Sync Environment

```bash
git clone https://github.com/lowkey999-netizen/genai-course-work.git
cd genai-course-work
uv sync
```

### 2. Run the Offline Test Suite

Run all verified offline unit and schema tests without needing API keys or incurring token costs:

```bash
uv run pytest tests/ showcase/ --ignore=tests/test_setup.py -k "not live and not estimate_matches and not test_model_answers" -v
```

### 3. Run with Live Providers (Optional)

To run live integration tests or launch notebooks against cloud and local models:

```bash
# Copy template and add your API keys (Groq, Gemini, or Ollama)
cp .env.example .env
uv run pytest
```
