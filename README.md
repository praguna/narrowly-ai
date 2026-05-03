# Narrowly AI

**Give your LLM access to specialist models that outperform it on specific tasks.**

Frontier LLMs are remarkable reasoners. But for certain tasks such as — extracting medications from clinical notes, parsing contract clauses, reading chart data etc — fine-tuned specialist models are faster, cheaper, and more accurate. The problem is finding them, trusting them, and calling them without building a custom pipeline.

Quiver solves this. It's an agent your LLM can query to discover and run vetted specialist models, then reason on top of the results.

---

## How It Works

Your LLM gets two capabilities:

**`quiver.query(task_description)`** — Describe what you need in plain language. Quiver searches a curated registry of specialist models and returns the best match, or tells you no specialist is available so your LLM can handle it itself.

**`quiver.execute(data, model_id)`** — Run the specialist. Get back structured output your LLM can reason on top of.

That's it. Your LLM decides when to delegate and when to handle things itself. Quiver just gives it the option.

---

## Example

```python
import quiver

# Your LLM calls this during reasoning
result = quiver.query("extract medication names and dosages from a clinical note")

# Quiver responds with a specialist that beats GPT-4o on this task
# {
#   "model_id": "allenai/medicine-ner",
#   "capability": "extracts medications, dosages, and frequencies from clinical text",
#   "beats_frontier_by": "18% F1 on clinical NER benchmarks",
#   "cost_per_call": "$0.0004",
#   "latency_p50": "180ms"
# }

# LLM decides to use it
output = quiver.execute(clinical_note, model_id="allenai/medicine-ner")

# LLM reasons on top of the structured output
```

If no specialist is available, Quiver says so and your LLM proceeds as normal. No disruption to your existing workflow.

---

## Access

**Python SDK** — call Quiver directly from your application code. Your LLM orchestration layer queries and executes specialists as part of its reasoning loop.

**MCP Server** — connect Quiver as a tool in any MCP-compatible agent (Claude, GPT-4o, and others). Your LLM gets `quiver_query` and `quiver_execute` as native tools it can invoke with no additional plumbing.

---

## Why Not Just Prompt the Frontier Model

You can. For low-volume tasks it's often fine. Quiver is worth it when:

- You're running thousands of structured extraction calls and cost adds up
- Accuracy on domain-specific entities matters more than good-enough
- You're spending significant prompt tokens on system prompts and few-shot examples to coax the right output

Quiver gives your LLM a way to delegate the parts it's not the best at, so it can focus on what it does best: reasoning.