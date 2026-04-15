<div align="center">

# Verum Intelligence
## Product and Implementation Overview (Frontend + Backend)

**Premium GCC regulatory intelligence workspace - client-facing technical overview of the current build state.**

[![Repository](https://img.shields.io/badge/Repository-Verum_Intelligence-0B1220?style=flat-square&logo=github)](https://github.com)
[![Architecture](https://img.shields.io/badge/Architecture-Next.js_%2B_Fastify-1F2937?style=flat-square)](#unified-tech-stack-and-runtime-services)
[![Status](https://img.shields.io/badge/Module_1-Live_Operational-0A7F3F?style=flat-square)](#module-1---ai-query-interface-operational-core)
[![License](https://img.shields.io/badge/License-Private-red?style=flat-square)](./LICENSE)

### Frontend Stack
[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat-square&logo=next.js)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)

### Backend Stack
[![Fastify](https://img.shields.io/badge/Fastify-5.x-000000?style=flat-square&logo=fastify)](https://fastify.dev)
[![Node.js](https://img.shields.io/badge/Node.js-22-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)
[![Zod](https://img.shields.io/badge/Zod-3.x-3E67B1?style=flat-square)](https://zod.dev)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL_%2B_Auth-3ECF8E?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![Upstash](https://img.shields.io/badge/Upstash-Redis_Guardrails-00E9A3?style=flat-square)](https://upstash.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-Responses_%2B_Embeddings-412991?style=flat-square&logo=openai&logoColor=white)](https://platform.openai.com)

</div>

This document unifies the current implementation reality across:

- `verum_FE` (Next.js frontend)
- `verum_BE` (Fastify backend)

It is intentionally explicit and conservative: **Module 1 (AI Query Interface) is the only fully operational end-to-end module at this stage**. The remaining product surfaces are designed, structurally prepared, and aligned for implementation, but are not yet live modules.

---

## Table of Contents

- [Overview](#overview)
- [Current Implementation Status](#current-implementation-status)
- [Why the Current Delivery Focus Matters](#why-the-current-delivery-focus-matters)
- [Module 1 - AI Query Interface (Operational Core)](#module-1---ai-query-interface-operational-core)
- [How Module 1 Works (Live Flow)](#how-module-1-works-live-flow)
- [Active Jurisdiction Coverage](#active-jurisdiction-coverage)
- [Unified Tech Stack and Runtime Services](#unified-tech-stack-and-runtime-services)
- [Frontend Routes and Backend API Surface](#frontend-routes-and-backend-api-surface)
- [Local Development Setup](#local-development-setup)
- [Environment Variables](#environment-variables)
- [Repository Scope and Delivery Standard](#repository-scope-and-delivery-standard)

---

## Overview

**Verum Intelligence** is a premium GCC regulatory intelligence workspace.  
For the current delivery phase, development has been intentionally focused on the single most critical product module: the **AI Query Interface**.

### Current implementation status

- **Operational now:** **Module 1 - AI Query Interface** (`/query` -> `POST /v1/query`)
- **Designed and ready for functional development upon project approval:** Dashboard, Comparison, Toolkit, Auth, Workspace, and Profile

This means the present build does **not** attempt to claim full operational parity across all product surfaces. Instead, it deliberately demonstrates the most important module **end-to-end** as the live functional core of the product for this delivery phase.

The current implementation follows the product direction defined in `PROJECT_SPEC.md` and `MODULE_1_AI_QUERY.md`:

- source-backed query first
- grounded retrieval and visible citations
- clear module boundaries
- disciplined, low-inflation architecture

The remaining modules are already resolved at the product-design and interface-architecture level, and are ready to move into functional implementation if the project is formally approved.

---

## Current Implementation Status

| Surface | Status | Notes |
|---|---|---|
| AI Query Interface | **Operational end-to-end** | Live FE/BE flow with retrieval, grounding, synthesis, citations, and explicit statuses |
| Compliance Dashboard | Scaffolded / mockup-aligned | Route and UI shell exist; backend intelligence layer remains staged |
| Framework Comparison | Scaffolded / mockup-aligned | Route and UI shell exist; normalized comparison logic remains staged |
| Market Entry Toolkit | Scaffolded / mockup-aligned | Route and UI shell exist; full backend-backed guidance remains staged |
| Auth | Demo-phase aligned | Honest placeholder access flow; production auth rollout remains staged |
| Workspace | Scaffolded / mockup-aligned | Shell exists; full continuity and persistence behavior remains staged |
| Profile | Scaffolded / mockup-aligned | Shell exists; production profile workflows remain staged |

---

## Why the Current Delivery Focus Matters

The present build intentionally demonstrates the highest-value and highest-risk module first.

Instead of distributing effort thinly across multiple incomplete product surfaces, the implementation has been concentrated on the one module that most directly proves the technical and product thesis of Verum Intelligence:

- natural-language regulatory query
- jurisdiction-aware retrieval
- source-backed grounding
- structured answer generation
- visible citations
- production-oriented runtime controls

This gives the current delivery real weight: it is not a cosmetic interface pass, but a live operational core that proves the most important backend and frontend integration path already works.

---

## Module 1 - AI Query Interface (Operational Core)

Module 1 is the live functional core of the current delivery.

What is already operational:

- Official endpoint: `POST /v1/query`
- Request validation and normalization
- Query guardrails (rate-limit and dedup) with explicit outcomes
- Retrieval orchestration plan
- Vector retrieval (`pgvector`)
- Exact/legal keyword retrieval (PostgreSQL full-text and SQL/RPC)
- Merge + rank of retrieval candidates
- Grounded context assembly
- Structured answer generation from grounded evidence
- Backend-generated citations
- Explicit result states:
  - `success`
  - `partial`
  - `no_results`
  - `rate_limited`
  - `validation_error`
  - `system_error`
- Frontend rendering of status semantics and citations
- Runtime prewarm/readiness hardening for first-run stability

In practical terms, this module already demonstrates the core behavior expected from the first live intelligence surface of the product.

---

## How Module 1 Works (Live Flow)

1. User submits a natural-language legal or compliance query from `/query`.
2. Optional jurisdiction scope is selected.
3. Frontend shapes and sends the request payload to backend `POST /v1/query`.
4. Backend validates payload shape and normalizes query input.
5. Runtime readiness checks and prewarm state are evaluated before retrieval proceeds.
6. Guardrails run when enabled to enforce rate-limit and request dedup behavior.
7. Retrieval plan is built from normalized input and jurisdiction scope.
8. Vector retrieval runs in Supabase PostgreSQL via `pgvector`.
9. Exact/legal keyword retrieval runs in Supabase PostgreSQL full-text and SQL/RPC paths.
10. Retrieval results are merged and ranked into a grounded candidate set.
11. Grounded context is assembled from retrieved source material only.
12. LLM synthesis generates structured output from grounded context only.
13. Backend attaches citations from source metadata rather than model-invented references.
14. Response is returned with explicit result-state semantics.
15. Frontend renders answer, citations, traceability, and response-state UI.
16. Query logging and persistence run where configured and applicable.

This is the live operational flow currently demonstrated in the build.

---

## Active Jurisdiction Coverage

Current active corpus depth for live Module 1 retrieval is focused on:

- **DIFC / DFSA**
- **ADGM / FSRA**

Planned expansion to QFC and KSA depends on extending ingestion, extraction, source normalization, and retrieval coverage in backend pipelines.

The next scale step is therefore **not** rebuilding Module 1 from scratch, but expanding the source and ingestion engine across the remaining target jurisdictions.

---

## Unified Tech Stack and Runtime Services

| Layer | Technology / Service | Used In | Why it exists | Current runtime function |
|---|---|---|---|---|
| Frontend framework | Next.js 15 | FE | App Router and production route composition | Marketing and product shell routes |
| UI runtime | React 19 | FE | Component and state model | Query UI and staged module shells |
| Styling | Tailwind CSS 3.4 | FE | Tokenized, maintainable styling | Premium interface system |
| API server | Fastify 5 | BE | Lean, explicit, high-performance API | Hosts `/health`, `/v1/query`, and staged module routes |
| Language | TypeScript 5.8 | FE + BE | Type-safe contracts and maintainability | Shared correctness across boundaries |
| Validation | Zod 3 | BE | Contract-safe parsing | Query request and response enforcement |
| Database platform | **Supabase / PostgreSQL** | BE core | Managed relational system of record | Stores corpus, chunks, citations, logs, and saved-query records |
| Vector retrieval | **pgvector (inside PostgreSQL)** | BE core | Semantic retrieval without separate vector vendor | Nearest-neighbor chunk retrieval for Module 1 |
| Exact retrieval | PostgreSQL full-text + SQL/RPC | BE core | Legal-term and exact-match recovery | Keyword branch in hybrid retrieval |
| LLM + embeddings | OpenAI API | BE core | Embeddings and grounded synthesis | Structured answer generation for Module 1 |
| Guardrails store | **Upstash Redis** | BE core | Fast ephemeral control plane | Rate-limit and dedup for query safety |
| FE auth/session SDK | Supabase JS | FE | Auth and session client primitives | Demo and staged auth plumbing in current phase |
| Build tooling | tsx + tsup + npm | FE + BE | Fast local dev and production builds | Dev servers and deploy artifacts |

### Supabase and Upstash Roles (Explicit)

- **Supabase/PostgreSQL is the durable product data backbone.**
  - Regulatory source records
  - Chunked retrieval corpus
  - Query logs and citations
  - Persistence supporting Module 1 behavior

- **Upstash Redis is the guardrails state layer.**
  - Rate-limit counters
  - Dedup windows
  - Ephemeral safety controls rather than durable product storage

---

## Frontend Routes and Backend API Surface

### Frontend Route Status

| Route | Status | Notes |
|---|---|---|
| `/` | Operational | Marketing entry surface |
| `/query` | **Operational** | Live Module 1 FE/BE integration |
| `/dashboard` | Scaffolded | Mockup-aligned shell |
| `/comparison` | Scaffolded | Mockup-aligned shell |
| `/toolkit` | Scaffolded | Mockup-aligned shell |
| `/workspace` | Scaffolded | Mockup-aligned shell |
| `/profile` | Scaffolded | Mockup-aligned shell |
| `/auth/login` | Demo-phase aligned | Honest placeholder access flow |
| `/auth/signup` | Demo-phase aligned | Honest placeholder access flow |

### Backend Endpoint Status

| Endpoint | Status | Notes |
|---|---|---|
| `GET /health` | Active | Runtime health verification |
| `POST /v1/query` | **Operational** | Live Module 1 pipeline |
| `GET /api/dashboard` | Scaffolded / placeholder | Staged module route |
| `GET /api/comparison` | Scaffolded / placeholder | Staged module route |
| `GET /api/toolkit` | Scaffolded / placeholder | Staged module route |
| `POST /api/auth/*` | Scaffolded / planned | Production auth remains staged |
| `GET /api/workspace` | Scaffolded / placeholder | Staged module route |
| `GET /api/profile` | Scaffolded / placeholder | Staged module route |

---

## Local Development Setup

### Prerequisites

- Node.js 22.x recommended
- npm 9.x or higher
- Supabase project
- OpenAI API key

### Run Backend

```bash
cd verum_BE
npm install
cp .env.example .env
npm run dev
```

Backend healthcheck:

```bash
curl http://localhost:4000/health
```

### Run Frontend

```bash
cd verum_FE
npm install
cp .env.local.example .env.local
npm run dev
```

Frontend URL:

- `http://localhost:3000`

---

## Environment Variables

### Frontend (`verum_FE/.env.local`)

```env
NEXT_PUBLIC_APP_NAME=Verum Intelligence
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000
NEXT_PUBLIC_QUERY_REQUEST_TIMEOUT_MS=45000
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### Backend (`verum_BE/.env`)

```env
PORT=4000
HOST=0.0.0.0
NODE_ENV=development

SUPABASE_URL=your_supabase_project_url
SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
SUPABASE_DB_URL=optional_database_url_for_tools

OPENAI_API_KEY=your_openai_api_key
OPENAI_CHAT_MODEL=gpt-5-mini
OPENAI_EMBEDDING_MODEL=text-embedding-3-small

QUERY_GUARDRAILS_MODE=auto
UPSTASH_REDIS_REST_URL=optional_if_guardrails_enabled
UPSTASH_REDIS_REST_TOKEN=optional_if_guardrails_enabled
QUERY_PREWARM_ENABLED=true
QUERY_PREWARM_TIMEOUT_MS=25000
QUERY_PREWARM_JURISDICTIONS=DIFC,ADGM
QUERY_PREWARM_EMBEDDING_ENABLED=true
```

Security rule:

- Never commit real secrets
- Keep only template and example env files in version control

---

## Repository Scope and Delivery Standard

### `verum_FE` owns

- Full landing page and product skin route UX UI
- Query page rendering and state semantics
- Typed client integration with backend contracts
- Demo and staged auth entry flow in the current phase

### `verum_BE` owns

- Query orchestration and retrieval pipeline
- Grounding, synthesis, and citations
- Supabase/PostgreSQL persistence and retrieval logic
- Upstash guardrails behavior
- Runtime readiness and prewarm controls

Delivery standard for current phase:

- clear module boundaries
- explicit status semantics
- source-backed outputs
- no fake parity claims for non-operational modules
- incremental expansion from Module 1 into remaining jurisdictions and modules
- implementation discipline over architectural theater
