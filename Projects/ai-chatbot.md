# Project: AI Chatbot (RAG)

> Build a production RAG chatbot over your team's docs.

---

## Goal

Build an AI chatbot that answers questions from your team's documentation, with citations, safely.

## Users
- **Team members** — ask questions, get answers with links.
- **Admins** — manage docs, monitor usage.

## Features (MVP)
- Ingest docs (markdown, PDF, web).
- Chunk + embed + store in vector DB.
- Chat interface (streaming).
- Retrieve relevant chunks per query.
- Answer with citations.
- Conversation history.

## Features (v2)
- Multi-user.
- Auth.
- Per-user doc access.
- Feedback (thumbs up/down).
- Eval dashboard.
- Cost tracking.
- Multiple model routing.

## Architecture

```
[Ingest]
  docs → chunk → embed → vector DB (pgvector)

[Query]
  user question → embed → vector search → top-K chunks → LLM (with citations) → stream answer
```

## Folder Structure
```
app/
  api/
    chat/route.ts            # streaming chat
    ingest/route.ts          # ingest docs
    search/route.ts          # vector search
  page.tsx                   # chat UI
components/
  Chat.tsx
  Message.tsx
  Source.tsx
lib/
  db.ts
  embeddings.ts
  chunks.ts
  rag.ts
content/
  docs/*.md
```

## Data Model
```sql
CREATE EXTENSION pgvector;

CREATE TABLE documents (
  id BIGSERIAL PRIMARY KEY,
  source TEXT NOT NULL,         -- file path or URL
  title TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE chunks (
  id BIGSERIAL PRIMARY KEY,
  document_id BIGINT REFERENCES documents(id) ON DELETE CASCADE,
  content TEXT NOT NULL,
  embedding VECTOR(1536),
  metadata JSONB,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX ON chunks USING ivfflat (embedding vector_cosine_ops) WITH (lists = 100);
```

## Tech Stack (verified)
- Next.js 15.
- Vercel AI SDK.
- OpenAI (`text-embedding-3-small`, `gpt-4o-mini`).
- Postgres + pgvector (Neon / Supabase).
- TypeScript strict.
- Tailwind + shadcn/ui.

## Chunking Strategy
- ~500-1000 tokens per chunk.
- ~100-200 token overlap.
- By paragraph / heading boundary.
- Preserve metadata (doc title, section, page).

## Embedding
```ts
import { openai } from '@ai-sdk/openai';
import { embedMany } from 'ai';

const { embeddings } = await embedMany({
  model: openai.embedding('text-embedding-3-small'),
  values: chunks.map(c => c.content),
});
```

## Vector Search
```sql
SELECT id, content, metadata, embedding <=> $1 AS distance
FROM chunks
ORDER BY embedding <=> $1
LIMIT 5;
```

## RAG Prompt
```
You are a helpful assistant. Answer the user's question using ONLY the provided context.

If the context doesn't contain the answer, say "I don't know based on the docs."

Cite sources as [1], [2], etc., matching the context numbering.

Context:
[1] {chunk_1}
[2] {chunk_2}
...

User question: {question}

Answer:
```

## AI Prompt

```
Build a RAG chatbot per /Projects/ai-chatbot.md.

Read first:
- /AI_AGENT_GUIDE.md
- /AI/README.md
- /AI/rag.md
- /LLM/README.md
- /Prompt-Engineering/README.md
- /Security/ai.md

Implement:
1. Ingest: read /content/docs/*.md, chunk, embed, store in pgvector.
2. Search: embed query, vector search top-5 chunks.
3. Chat: stream LLM response with citations.
4. UI: chat interface with source links.
5. Cost tracking (per request).
6. Rate limiting per user.
7. Sanitize user input (prompt injection).
8. Output validation (citations format).

Use Vercel AI SDK + OpenAI + pgvector.
Stream tokens. Show source links under each answer.
Run /Checklists/pre-launch.md before reporting done.
```

## Challenges
- **Chunking** — too small loses context, too big dilutes.
- **Retrieval quality** — try hybrid (vector + keyword).
- **Citations** — LLM may hallucinate. Validate.
- **Cost** — embedding + LLM tokens add up. Cache.
- **Prompt injection** — sanitize user content.
- **Freshness** — re-ingest when docs change.
- **Eval** — don't ship without measuring quality.

## Extensions
- Hybrid search (vector + BM25).
- Reranking (Cohere, Voyage).
- Multi-modal (images, PDFs).
- Per-user doc permissions.
- Feedback collection + eval dashboard.
- Model routing (cheap model for simple Qs).

## Checklist
- [ ] Evals pass (10 known Q/A pairs).
- [ ] Citations are real (not hallucinated).
- [ ] Cost per query < $0.01.
- [ ] Streaming first token < 1s.
- [ ] Prompt injection tested.
- [ ] Rate limited.
- [ ] No PII in logs.

## References
- Vercel AI SDK RAG: https://sdk.vercel.ai/docs/guides/rag-chatbot
- pgvector: https://github.com/pgvector/pgvector
- Anthropic contextual retrieval: https://www.anthropic.com/news/contextual-retrieval

---

**Next:** [saas.md](saas.md) · Back to [Projects/](README.md)
