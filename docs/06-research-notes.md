# 06 Research notes

_Collected 9 Oct 2026 from web searches. Most figures are vendor- or blog-reported and this space moves fast. Verify before relying on them._

## Jev (decision model)

- A decision model from the startup TypeSafe AI. It reads language like an LLM but cannot write replies, code or explanations; it picks from options you supply and returns probabilities.
- Reported pricing: $0.042 per million input tokens, with free output.
- Reported release date: 15 September 2026. Offered as a hosted API; no downloadable weights were found.
- Useful pattern: LLM writes, Jev decides (typed Choice/Score with probabilities), plain code acts.
- Good fits: model routing, guard/permission checks, intent routing, confidence-gated escalation.
- A paper on using JEV as a judge reports that accepting confident verdicts and escalating uncertain ones retained about 99% of a frontier LLM judge's accuracy at a tiny fraction of the cost.

**Caveats**

- Savings apply to decision calls, not to code generation itself.
- Weaker on reasoning-heavy judgements: reported 14.6 points behind on JudgeBench; one comparison showed 62.6% against 81.3% for a small Claude model on a broad phishing question.
- New and mostly vendor-reported: test on your own data.
- Documented limitation: injected instructions, or text arguing for its own classification, can move the answer. Do not make it the only gate for destructive actions.
- It is not a drop-in model swap; it lives inside your harness.

## Local models (Apple Silicon)

RAM (unified memory) is what limits local models, not SSD size. M4 MacBooks go up to 32GB (M4), 48GB (M4 Pro) and 128GB (M4 Max).

| RAM | Reported pick |
|---|---|
| 16GB | Qwen 3.5-9B (Q4) |
| 24GB | Qwen 3.6-27B |
| 32GB+ | Qwen 3.6-35B-A3B or Qwen3-Coder-30B-A3B (about 19 GB) |
| 64GB+ | Qwen3-Coder-Next (Q4) |

- Runtimes: Ollama (MLX preview backend in recent versions), LM Studio or `mlx_lm`; all expose OpenAI-compatible endpoints.
- Tool-calling reliability varies by runtime; test it yourself.
- Local 27-35B models handle routine edits well but trail frontier models on hard multi-file agentic work, which is what a router is for.

## Agent frameworks (summary)

| Framework | Notes |
|---|---|
| Pydantic AI | Type-safe, model-agnostic, durable execution; younger multi-agent story |
| LangGraph | Stateful graphs, checkpointing; steeper curve |
| Claude Agent SDK | Coding-agent primitives, strong MCP support; Claude-only |
| OpenAI Agents SDK | Simple; 100+ models via LiteLLM |
| CrewAI | Role-based multi-agent; adds token cost |

## Visual builder landscape

- Flowise, Langflow, n8n and Dify offer drag-and-drop agent builders; all four are open-source with free self-hosting.
- Dify reports 130K+ GitHub stars and 100+ LLM providers.
- OpenAI's AgentKit includes a visual Agent Builder.
- Google Vertex AI Agent Builder and Microsoft Copilot Studio cover the enterprise side.

## Name check

"patchbay" was considered and rejected: several existing GitHub projects already use it, including AI-related ones. Always check GitHub, PyPI, npm and domains before settling on a name.

## Sources

- Jev: https://datanorth.ai/blog/jev-what-it-is-and-why-this-new-model-matters
- Jev: https://www.respan.ai/articles/what-is-the-jev-ai-model
- Jev: https://pooyagolchian.com/blog/what-is-jev-ai-decision-model-2026/
- Jev: https://www.aibuilderclub.com/blog/jev-engineering-guide
- Jev as judge: https://aiweekly.co/alerts/jev-judge-model-matches-llm-accuracy-at-036-of-the-cost
- Local models: https://stridenote.net/best-local-llms-coding-2026/
- Local models: https://ollamaherd.com/guides/apple-silicon-models
- Frameworks: https://www.morphllm.com/ai-agent-framework
- Frameworks: https://devtoollab.com/blog/best-ai-agent-frameworks
- Builders: https://fast.io/resources/best-no-code-ai-agent-builders/
- Builders: https://rasa.com/blog/best-low-code-ai-agents-platforms-for-2026
- Builders: https://www.morphllm.com/no-code-ai-agent
- Builders: https://inkeep.com/blog/agent-frameworks-platforms-overview
