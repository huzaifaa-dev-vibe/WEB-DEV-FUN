# Prompt Engineering

> Structured prompting. Evals. Patterns for reliable LLM output.

---

## Purpose

Master prompt engineering for production AI features.

## Prerequisites

- [LLM/](../LLM/), [AI/](../AI/).

## Learning Outcome

You can write prompts that produce reliable, validated output.

## Dependencies

- An LLM API.

## Related Files

- [PROMPTS.md](../PROMPTS.md) · [AI/](../AI/) · [LLM/](../LLM/) · [Prompt-Engineering/patterns.md](patterns.md) · [Prompt-Engineering/evals.md](evals.md)

## AI Instructions

When writing prompts:
1. **Be specific**. Vague → vague.
2. **Give examples** (few-shot).
3. **Define the role** (system prompt).
4. **Define output format** (JSON schema).
5. **Define constraints** (length, tone, content).
6. **Iterate with evals.**
7. **Version prompts** like code.
8. **Test against adversarial inputs.**

## Human Notes

### Anatomy of a good prompt
```
[ROLE] You are a customer support agent for Acme Inc.

[TASK] Categorize the user's message into one of:
- billing
- technical
- general
- complaint

[CONTEXT] Acme Inc. is a SaaS company. Recent outages: ...

[EXAMPLES]
User: "I can't log in"
Category: technical

User: "Why was I charged twice?"
Category: billing

[INPUT] {user_message}

[OUTPUT FORMAT] JSON: { "category": "...", "confidence": 0-1, "reasoning": "..." }

[CONSTRAINTS]
- Confidence > 0.7 required.
- If unclear, choose "general".
- Don't include any text outside the JSON.
```

### Patterns

#### Few-shot
Provide examples in the prompt. Improves accuracy.

#### Chain-of-thought
"Think step by step." before answer. Improves reasoning.

#### Self-critique
Ask LLM to critique its own answer, then revise.

#### Decomposition
Break complex task into subtasks, solve each.

#### Tree of thoughts
Explore multiple paths, pick best.

#### ReAct
Reason + Act in a loop. (Agent pattern.)

→ [Prompt-Engineering/patterns.md](patterns.md)

### Structured output
Force JSON:
```
Respond with valid JSON matching this schema:
{ "name": string, "age": number }
```
Or use `response_format` API.
Or use Vercel AI SDK `generateObject` with Zod.

### Prompt injection defense
- Treat user content as data, not instructions.
- Use delimiters: `User input: """{user_input}"""`
- Filter for "ignore previous instructions" patterns (imperfect).
- Use separate system message.
- Validate output.

→ [Security/ai.md](../Security/ai.md)

### Versioning
- Prompts are code.
- Version them (git).
- Tag with eval results.
- Roll back if regression.

### Evals
- Test prompts against known inputs.
- Track metrics.
- Run on every prompt change.

→ [Prompt-Engineering/evals.md](evals.md)

### Cost optimization
- Smaller model when possible.
- Fewer tokens (concise prompt).
- Caching.
- Don't repeat context (cache it).

### Multimodal prompts
- Vision: send image + text.
- Audio: transcribe first, then prompt.

### Common patterns
- **Summarization**: "Summarize this in 3 bullets: {text}"
- **Extraction**: "Extract entities as JSON: {text}"
- **Classification**: "Classify as A/B/C: {text}"
- **Translation**: "Translate to French: {text}"
- **Code generation**: "Write a function that..."
- **Code review**: "Review this code for..."

### Tools / function calling
- Define tools clearly.
- Description matters (LLM reads it).
- Validate inputs (Zod).

### Streaming
- Stream tokens for UX.
- Use partial JSON parsing for structured output.

## Common Mistakes

- ❌ Vague prompts.
- ❌ No examples.
- ❌ No output format.
- ❌ No evals.
- ❌ Trusting output without validation.
- ❌ Prompt injection vulnerability.
- ❌ Not iterating.
- ❌ No versioning.

## Tools

- OpenAI Playground: https://platform.openai.com/playground
- Anthropic Console: https://console.anthropic.com/
- Promptfoo: https://www.promptfoo.dev/
- LangSmith: https://smith.langchain.com/
- Braintrust: https://www.braintrust.dev/
- Vercel AI SDK: https://sdk.vercel.ai/

## References

- Prompting Guide: https://www.promptingguide.ai/
- Learn Prompting: https://learnprompting.org/
- Anthropic prompting: https://docs.anthropic.com/claude/docs/prompt-engineering
- OpenAI prompting: https://platform.openai.com/docs/guides/prompt-engineering

## Further Reading

- *Prompt Engineering Guide* (free): https://www.promptingguide.ai/

## Exercises

1. Write a classification prompt. Eval on 50 examples.
2. Add few-shot examples. Re-eval.
3. Add structured output. Validate with Zod.

## Projects

- Build an eval harness for your prompts.

---

**Previous:** [Agentic-Coding/](../Agentic-Coding/) · **Next:** [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · **Related:** [PROMPTS.md](../PROMPTS.md)
