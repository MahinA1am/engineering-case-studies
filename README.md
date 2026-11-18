# Engineering case studies

Most of my professional work lives in private company repositories, so the code can't be shown. These pages describe what I built instead: the problem, the design, the hardest bug and the result.

All of this was built in 2026 at an early-stage startup making an AI workspace for sales and go-to-market teams. Company names, customers, internal identifiers and anything that could expose a security weakness are left out. No proprietary code is included.

| # | Case study | What it shows |
|---|---|---|
| 1 | [Usage-based billing and a credit ledger](01-usage-based-billing.md) | Stripe, idempotent money movement, PostgreSQL, debugging in production |
| 2 | [An MCP server for AI assistants](02-mcp-server.md) | API design, OAuth 2.1, long-running sessions, protocol compliance |
| 3 | [Evaluating LLMs before switching models](03-llm-evaluation.md) | LLM evaluation, structured output, cost and latency |
| 4 | [An AI meeting notetaker](04-ai-meeting-notetaker.md) | Third-party integrations, webhooks, race conditions, background workflows |
| 5 | [An AI content-automation pipeline](05-content-automation-pipeline.md) | Greenfield full-stack build, vector search, LLM-as-judge, Docker deploy |
| 6 | [Hardening a multi-tenant SaaS](06-multi-tenant-security.md) | Tenant isolation, SSRF protection, token handling |
| 7 | [One data path for a messaging inbox](07-inbox-data-and-sync.md) | Frontend data architecture, sync pipelines, deleting code |

**Stack across these projects:** TypeScript, Next.js and React, Node.js, Temporal, PostgreSQL (Supabase), Redis, Stripe, Docker, Railway, the Anthropic and OpenAI APIs, Vitest and Playwright.

**Contact:** [LinkedIn](https://linkedin.com/in/mahin-alam1) · [GitHub](https://github.com/MahinA1am)
