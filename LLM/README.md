# LLM

> Large Language Models. Models, context, sampling, function calling, routing.

---

## Purpose

Understand LLMs deeply: how they work, how to use them, how to pick them.

## Prerequisites

- Basic AI/ML interest, [AI/](../AI/).

## Learning Outcome

You can pick the right model, configure sampling, use function calling, route by task.

## Dependencies

- An LLM provider.

## Related Files

- [AI/](../AI/) · [Prompt-Engineering/](../Prompt-Engineering/) · [MCP/](../MCP/) · [LLM/context.md](context.md) · [LLM/routing.md](routing.md)

## AI Instructions

When picking models:
1. **Start with smallest** that could work.
2. **Verify with evals** before scaling up.
3. **Use larger model only when smaller fails evals.**
4. **Consider latency + cost** in addition to quality.

## Human Notes

### Model families (as of 2025)

#### Proprietary
- **OpenAI**: GPT-4o, GPT-4o-mini, o1, o3-mini.
- **Anthropic**: Claude 3.5 Sonnet, Haiku, Opus.
- **Google**: Gemini 2.0 Flash, Pro.
- **xAI**: Grok-3, Grok-2.
- **Meta (via partners)**: Llama 3.3.

#### Open-source / open-weights
- **Llama 3.3** (Meta).
- **Qwen 2.5** (Alibaba).
- **Mistral** / **Mixtral**.
- **DeepSeek V3 / R1**.
- **Gemma 2** (Google).
- **Phi** (Microsoft).

### How to pick
| Need | Pick |
|---|---|
| Best quality, cost no object | GPT-4o / Claude 3.5 Sonnet |
| Cheap + fast + good | GPT-4o-mini / Claude 3.5 Haiku / Gemini 2.0 Flash |
| Open-source, self-host | Llama 3.3 70B / Qwen 2.5 / DeepSeek V3 |
| Reasoning | o1 / o3-mini / DeepSeek R1 / Claude with thinking |
| Long context (1M+) | Gemini 2.0 Pro |
| Code | Claude 3.5 Sonnet / GPT-4o / DeepSeek Coder |
| Vision | GPT-4o / Claude 3.5 / Gemini 2.0 |

### Context window
- Llama 3: 128k.
- GPT-4o: 128k.
- Claude 3.5: 200k.
- Gemini 2.0 Pro: 2M.

More context = more cost. Don't stuff everything in.

→ [LLM/context.md](context.md)

### Sampling parameters
- `temperature` (0–2): higher = more random. 0 = deterministic.
- `top_p` (0–1): nucleus sampling. 0.9 = top 90% probability mass.
- `top_k`: top K tokens. Less common.
- `max_tokens`: limit output.
- `stop`: stop sequences.
- `frequency_penalty` / `presence_penalty`: discourage repetition.

Rule of thumb:
- Classification / extraction: temp 0.
- Conversation: temp 0.7.
- Creative: temp 0.9+.

### Function calling / tool use
LLM calls your functions:
```ts
const tools = [{
  type: 'function',
  function: {
    name: 'get_weather',
    description: 'Get weather',
    parameters: {
      type: 'object',
      properties: { city: { type: 'string' } },
      required: ['city'],
    },
  },
}];
```
LLM returns: `{ name: 'get_weather', arguments: { city: 'NYC' } }`.

### Structured output
Force JSON output:
```ts
{
  response_format: { type: 'json_object' }
}
```
Or with schema (some providers):
```ts
{
  response_format: {
    type: 'json_schema',
    json_schema: { name: 'user', schema: { ... } },
  }
}
```

Or use Vercel AI SDK `generateObject` with Zod.

### Routing
Use different models for different tasks:
- Simple classification → cheap model.
- Complex reasoning → expensive model.
- Code → code-specialized model.

→ [LLM/routing.md](routing.md)

### Embeddings
- Convert text → vector.
- For RAG, semantic search, clustering.
- Models: `text-embedding-3-small/large` (OpenAI), `voyage-3` (Voyage), `bge-m3` (open).
- Dimension: 256 to 4096.
- Store in vector DB (pgvector, Qdrant, etc.).

### Fine-tuning
- When prompting + RAG isn't enough.
- LoRA / QLoRA for cheap fine-tuning.
- Most apps don't need it. Start with prompting + RAG.

### Multimodal
- GPT-4o, Claude 3.5, Gemini 2.0 all support vision.
- Some support audio (Gemini).

### Cost
- Per million tokens (input + output).
- Output usually 2-4x input cost.
- Cache to reduce.
- Use smaller model when possible.

### Latency
- Cold start: 1-3s.
- Streaming first token: <500ms.
- Full response: 1-30s depending on length.

### Provider comparison
| | OpenAI | Anthropic | Google | Open-source |
|---|---|---|---|---|
| Best model | GPT-4o | Claude 3.5 Sonnet | Gemini 2.0 Pro | Llama 3.3 70B |
| Cheapest | GPT-4o-mini | Haiku | Flash | (self-host) |
| Long context | 128k | 200k | 2M | varies |
| Tool use | ✅ | ✅ | ✅ | varies |
| Vision | ✅ | ✅ | ✅ | varies |
| Self-host | ❌ | ❌ | ❌ | ✅ |

### OpenRouter
Access all providers via one API: https://openrouter.ai/

### Local LLMs
- **Ollama** — easiest local runner.
- **LM Studio** — GUI.
- **llama.cpp** — low-level.

For dev / privacy / experimentation.

## Common Mistakes

- ❌ Using GPT-4 when mini suffices.
- ❌ No caching.
- ❌ No streaming.
- ❌ Stuffing everything in context.
- ❌ No evals.
- ❌ Trusting output without validation.
- ❌ Ignoring cost.

## Tools

- OpenAI playground: https://platform.openai.com/playground
- Anthropic console: https://console.anthropic.com/
- OpenRouter: https://openrouter.ai/
- Ollama: https://ollama.com/
- LM Studio: https://lmstudio.ai/

## References

- Hugging Face blog: https://huggingface.co/blog
- Sebastian Raschka's magazine: https://magazine.sebastianraschka.com/
- Latent Space: https://www.latent.space/
- The Batch: https://www.deeplearning.ai/the-batch/

## Further Reading

- *Build a Large Language Model (From Scratch)* — Sebastian Raschka
- *Hands-On Large Language Models* — Jay Alammar, Maarten Grootendorst
- *AI Engineering* — Chip Huyen

## Exercises

1. Compare GPT-4o-mini vs Haiku on your task (eval).
2. Implement function calling.
3. Implement structured output with Zod.

## Projects

- Build a model-routing layer that picks cheapest sufficient model per task.

---

**Previous:** [AI/](../AI/) · **Next:** [MCP/](../MCP/) · **Related:** [Prompt-Engineering/](../Prompt-Engineering/)
