# Narrowly AI

**A capability layer that gives any LLM access to the best tool or model for a specific task.**

LLMs are great at reasoning — not always at executing. Specialist models and purpose-built tools exist that are faster, cheaper, and more accurate for structured tasks. **Quiver** gives your LLM a single interface to dynamically discover and run them.

One meta-tool instead of hundreds of statically defined integrations. New capabilities available instantly with no code changes.

---

## How It Works

**`quiver.query(task_description)`** — Describe the task in plain language. Returns the best match from the registry, or `no_match` so your LLM handles it itself.

**`quiver.execute(data, capability_id)`** — Run it. Get back structured output your LLM can reason on top of.

---

## Example

```python
import quiver

result = quiver.query("extract medication names and dosages from clinical text")
# {
#   "capability_id": "clinical-ner-v1",
#   "type": "model",
#   "description": "extracts medications, dosages, and frequencies from clinical text",
#   "outperforms_frontier_by": "18% F1 on clinical NER benchmarks",
#   "cost_per_call": "$0.0004",
#   "latency_p50": "180ms"
# }

output = quiver.execute(clinical_note, capability_id="clinical-ner-v1")

# Works the same for tools
result = quiver.query("normalize this date string to ISO 8601")
# { "capability_id": "date-normalizer-v1", "type": "tool", "latency_p50": "3ms" }
```

If nothing fits, Quiver returns `no_match`. Your LLM proceeds as normal.

---

## Access

**Python SDK** — integrate directly into your application or LLM orchestration layer.

**MCP Server** — works with Claude, GPT-4o, and any MCP-compatible model out of the box.

---

## Why Not Statically Define Everything

Quiver is worth it when:

- Your LLM needs many capabilities and static tool lists become unwieldy
- You want new capabilities available instantly without code changes
- You are running high-volume structured tasks where cost and accuracy matter
- Your LLM is small or on-device and needs to offload tasks it handles poorly
- You need specialists running locally without data leaving your environment
