# AI

> LLMs in web apps. RAG, agents, evals, cost, safety.

---

## Purpose

Build LLM-powered features that don't hallucinate, don't get abused, and don't bankrupt you.

## Prerequisites

- [Backend/](../Backend/), basic LLM understanding.

## Learning Outcome

You can ship production AI features safely.

## Dependencies

- An LLM API (OpenAI, Anthropic, etc.).

## Related Files

- [LLM/](../LLM/) · [MCP/](../MCP/) · [Agentic-Coding/](../Agentic-Coding/) · [Prompt-Engineering/](../Prompt-Engineering/) · [PROMPTS.md](../PROMPTS.md) · [Security/ai.md](../Security/ai.md) · [Performance/ai-cost.md](../Performance/ai-cost.md) · [AI/rag.md](rag.md) · [AI/agents.md](agents.md) · [AI/evals.md](evals.md)

## AI Instructions

When building AI features:
1. **Pick smallest model that works.** → [LLM/routing.md](../LLM/routing.md)
2. **Stream tokens.** Users hate waiting.
3. **Cache aggressively.** Same prompt → same response.
4. **Validate output** with schema (Zod).
5. **Rate-limit per user.**
6. **Log everything** (prompt, response, cost).
7. **Have a fallback** when LLM is down.
8. **Evals before you ship.** → [AI/evals.md](evals.md)
9. **Sanitize user input** for prompt injection. → [Security/ai.md](../Security/ai.md)
10. **Cost-monitor** every endpoint.

## Human Notes

### AI features by complexity
1. **Single-call** — prompt → response. (Chat, summarize, classify.)
2. **Structured output** — prompt → JSON (Zod-validated).
3. **Function calling** — LLM calls your tools.
4. **RAG** — retrieve context, then answer.
5. **Agent** — LLM plans + executes + reflects.
6. **Multi-agent** — multiple LLMs cooperate.

### RAG (Retrieval-Augmented Generation)
- Index docs (embeddings + vector DB).
- At query: retrieve relevant chunks.
- Stuff into prompt.
- LLM answers.

→ [AI/rag.md](rag.md)

### Agents
- LLM with tools.
- Loop: think → act → observe → repeat.
- Tools: search, code exec, file I/O, API calls.
- Frameworks: LangChain, Mastra, OpenAI Assistants, Vercel AI SDK.

→ [AI/agents.md](agents.md)

### Evals
- Don't ship without them.
- Test prompts against known inputs.
- Track metrics (accuracy, helpfulness, safety).
- Run on every prompt change.

→ [AI/evals.md](evals.md)

### Cost management
- Per-user cost tracking.
- Cache.
- Smaller models.
- Hard limits.
- Alerts.

→ [Performance/ai-cost.md](../Performance/ai-cost.md)

### Safety
- **Prompt injection** — user content as data, not instructions.
- **Output validation** — schema + sanity.
- **PII redaction** in logs.
- **Rate limiting**.
- **Abuse detection**.
- **Human-in-the-loop** for high-stakes.

→ [Security/ai.md](../Security/ai.md)

### Streaming
- Stream tokens to user (better UX).
- Use SSE or WebSocket.
- Vercel AI SDK handles this.

### Tools / Function calling
```ts
const tools = {
  get_weather: {
    description: 'Get weather for a city',
    parameters: z.object({ city: z.string() }),
    execute: async ({ city }) => fetchWeather(city),
  },
};

const result = await generateText({
  model: openai('gpt-4o-mini'),
  tools,
  messages: [{ role: 'user', content: 'Weather in NYC?' }],
});
```

### Structured output
```ts
const { object } = await generateObject({
  model: openai('gpt-4o-mini'),
  schema: z.object({ name: z.string(), age: z.number() }),
  prompt: 'Extract from: John is 30',
});
```

### Caching
- Same prompt + model + temp = same response (within TTL).
- Semantic cache (similar prompt = cached response).
- Use Vercel AI SDK `experimental_telemetry` + cache.

### Common stacks
- **Vercel AI SDK** (TS) — best DX.
- **LangChain.js** — full-featured, complex.
- **Mastra** — TS agent framework.
- **Instructor** — structured extraction.
- **LlamaIndex** (Python, RAG-focused).
- **DSPy** (Python, programmatic).

## Common Mistakes

- ❌ No evals.
- ❌ No output validation.
- ❌ Prompt injection vulnerability.
- ❌ No cost monitoring.
- ❌ No streaming.
- ❌ Big model when small suffices.
- ❌ No fallback.
- ❌ No rate limiting.
- ❌ Logging PII.
- ❌ Trusting LLM output blindly.

## Tools

- Vercel AI SDK: https://sdk.vercel.ai/
- LangChain: https://js.langchain.com/
- LlamaIndex: https://docs.llamaindex.ai/
- Mastra: https://mastra.ai/
- OpenAI: https://platform.openai.com/docs
- Anthropic: https://docs.anthropic.com/
- OpenRouter: https://openrouter.ai/
- Ollama: https://ollama.com/
- Instructor: https://instructor-js.devinim.com/

## References

- Vercel AI SDK docs: https://sdk.vercel.ai/docs
- Anthropic cookbook: https://github.com/anthropics/anthropic-cookbook
- OpenAI cookbook: https://github.com/openai/openai-cookbook
- Latent Space: https://www.latent.space/

## Further Reading

- *AI Engineering* — Chip Huyen
- *Hands-On Large Language Models* — Alammar, Grootendorst
- *Designing Machine Learning Systems* — Chip Huyen

## Exercises

1. Build a RAG over your docs.
2. Add evals.
3. Add structured output.
4. Add streaming.

## Projects

- Build a production RAG chatbot for your team's docs.

---

**Previous:** [E2E/](../E2E/) · **Next:** [LLM/](../LLM/) · **Related:** [MCP/](../MCP/), [Agentic-Coding/](../Agentic-Coding/)
