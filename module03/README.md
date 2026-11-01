# Module 03: LLM Applications

> _Built while following Ajit Byru's GenAI / Agentic AI course._

This module explores multi-turn conversational state, context window economics, function calling mechanics, and orchestrating stateful tool execution pipelines with LangChain.

---

## Module Pipeline Architecture

```text
                    ╭──────────────────────╮
                    │     User Dialogue    │
                    ╰──────────┬───────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │     Chat State & Memory Pipeline     │
            │  Messages List · Sliding vs Summary  │
            ╰──────────────────┬───────────────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │    Context Ceiling & Token Budget    │
            │   Hard Window Limits · Eviction      │
            ╰──────────────────┬───────────────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │      Tool & Intent Dispatcher        │
            ╰───────┬──────────────────────┬───────╯
                    │ Direct (Text)        │ Tool Calling
                    ▼                      ▼
            ╭───────────────╮      ╭───────────────╮
            │ Direct Reply  │      │ Tool Engine   │
            │ Conversational│      │ JSON Schema   │
            ╰───────┬───────╯      ╰───────┬───────╯
                    │                      │
                    ╰──────────┬───────────╯
                               │
                               ▼
            ╭──────────────────────────────────────╮
            │      Agent Orchestrator (LangChain)  │
            │  State Loop · Tool Output Injection  │
            ╰──────────────────┬───────────────────╯
                               │
                               ▼
                    ╭──────────────────────╮
                    │ Verified Multi-Turn  │
                    │   Assistant Output   │
                    ╰──────────────────────╯
```

---

## Session Directory & Artifacts

| Session | Core Lab Notebook | Key Helpers & Resources | Deliverables & Artifacts | Test Suite |
| :--- | :--- | :--- | :--- | :--- |
| **Session 19: Chat State & Memory Windows** | [`s19_chat_memory.ipynb`](./s19_chat_memory.ipynb) | • [`chat_utils.py`](./chat_utils.py)<br>• [`chat_tasks.py`](./chat_tasks.py)<br>• [`terms_s19.md`](./terms_s19.md) | • [`experiments/s19_chat_memory.md`](../experiments/s19_chat_memory.md) | [`tests/test_s19.py`](../tests/test_s19.py) |

---

## What I Learned

- **Session 19 (Chat State & Memory):** Benchmarked Naive (full history), Sliding Window ($K=6$), and Progressive Summarization across a 17-turn scripted dialogue (`RECALL_PROBE`) with an account reference token (`77042`) planted at turn 2. The Naive baseline recalled the token successfully but token cost escalated to 1,866 tokens on turn 17 ($O(N^2)$ cumulative trajectory). A 6-turn sliding window trimmed the final-turn cost by 45.8% (1,011 tokens) but suffered deterministic amnesia on early state. Progressive summarization reduced final-turn cost by 27.8% (1,348 tokens) across 2 auxiliary compression calls, but lost the exact reference token in lossy summarization without explicit entity retention.

---

## Running Module 03 Tests

Verify all module checkpoints offline:

```bash
# Run all deterministic offline tests across Module 03:
uv run pytest tests/test_s19.py -k "not live" -v
```
