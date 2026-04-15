<div align="center">

# Verum Intelligence
## Unified Platform README (Frontend + Backend)

**Premium GCC regulatory intelligence workspace - unified technical reference for FE and BE.**

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

It is intentionally explicit and conservative: **Module 1 (AI Query Interface) is the only fully operational end-to-end module right now**. Other module surfaces are scaffolded, staged, or demo-aligned depending on route.

---

## Table of Contents

- [Overview](#overview)
- [Current Implementation Status](#current-implementation-status)
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
Current practical delivery is centered on one live nucleus:

- **Operational now:** Module 1 - AI Query Interface (`/query` -> `POST /v1/query`)
- **Staged/scaffolded:** Dashboard, Comparison, Toolkit, Auth, Workspace, Profile

This architecture follows the product direction defined in `PROJECT_SPEC.md` and `MODULE_1_AI_QUERY.md`:

- source-backed query first
- grounded retrieval + citations
- clear module boundaries
- disciplined, low-inflation architecture

---

## Current Implementation Status

| Surface | Status | Notes |
|---|---|---|
| AI Query Interface | **Operational end-to-end** | Live FE/BE flow with retrieval, grounding, synthesis, citations, explicit statuses |
| Compliance Dashboard | Scaffolded / mockup-aligned | Route and UI shell exist; backend intelligence staged |
| Framework Comparison | Scaffolded / mockup-aligned | Route and UI shell exist; normalized comparison logic staged |
| Market Entry Toolkit | Scaffolded / mockup-aligned | Route and UI shell exist; full backend-backed guidance staged |
| Auth | Demo-phase aligned | Honest placeholder flow; production auth rollout staged |
| Workspace | Scaffolded / mockup-aligned | Shell exists; full continuity behavior staged |
| Profile | Scaffolded / mockup-aligned | Shell exists; production profile workflows staged |

---

## Module 1 - AI Query Interface (Operational Core)

Module 1 is the live functional core of the current milestone.

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
- Frontend rendering of status semantics + citations
- Runtime prewarm/readiness hardening for first-run stability

---

## How Module 1 Works (Live Flow)

1. User submits a natural-language legal/compliance query from `/query`.
2. Optional jurisdiction scope is selected.
3. Frontend shapes and sends payload to backend `POST /v1/query`.
4. Backend validates payload and normalizes query input.
5. Runtime readiness checks/prewarm are evaluated before retrieval.
6. Guardrails run (Upstash Redis) when enabled.
7. Retrieval plan is built.
8. Vector retrieval runs in Supabase PostgreSQL via `pgvector`.
9. Exact/legal keyword retrieval runs in Supabase PostgreSQL full-text/SQL.
10. Results are merged and ranked.
11. Grounded context is assembled from retrieved sources.
12. LLM synthesizes structured output from grounded context only.
13. Backend attaches citations from source metadata.
14. Response returns with explicit status semantics.
15. Frontend renders answer, citations, and result-state UI.
16. Query persistence/logging runs where configured.

---

## Active Jurisdiction Coverage

Current active corpus depth for live Module 1 retrieval is focused on:

- **DIFC / DFSA**
- **ADGM / FSRA**

Planned expansion to QFC and KSA depends on extending ingestion/extraction/source normalization/retrieval coverage in backend pipelines.

---

## Unified Tech Stack and Runtime Services

| Layer | Technology / Service | Used In | Why it exists | Current runtime function |
|---|---|---|---|---|
| Frontend framework | Next.js 15 | FE | App Router + production route composition | Marketing + product shell routes |
| UI runtime | React 19 | FE | Component/state model | Query UI + module shells |
| Styling | Tailwind CSS 3.4 | FE | Tokenized, maintainable styling | Premium interface system |
| API server | Fastify 5 | BE | Lean, explicit, high-performance API | Hosts `/health`, `/v1/query`, staged routes |
| Language | TypeScript 5.8 | FE + BE | Type-safe contracts and maintainability | Shared correctness across boundaries |
| Validation | Zod 3 | BE | Contract-safe parsing | Query request/response enforcement |
| Database platform | **Supabase / PostgreSQL** | BE core | Managed relational system of record | Stores corpus, chunks, citations, logs, saved query records |
| Vector retrieval | **pgvector (inside PostgreSQL)** | BE core | Semantic retrieval without separate vector vendor | Nearest-neighbor chunk retrieval for Module 1 |
| Exact retrieval | PostgreSQL full-text + SQL/RPC | BE core | Legal-term and exact-match recovery | Keyword branch in hybrid retrieval |
| LLM + embeddings | OpenAI API | BE core | Embeddings + grounded synthesis | Structured query answer generation |
| Guardrails store | **Upstash Redis** | BE core | Fast ephemeral control plane | Rate-limit + dedup for query safety |
| FE auth/session SDK | Supabase JS | FE | Auth/session client primitives | Demo/staged auth plumbing in current phase |
| Build tooling | tsx + tsup + npm | FE + BE | Fast local dev + production builds | Dev servers and deploy artifacts |

### Supabase and Upstash Roles (Explicit)

- **Supabase/PostgreSQL is the durable product data backbone.**
  - Regulatory source records
  - Chunked retrieval corpus
  - Query logs and citations
  - Persistence supporting Module 1 behavior
- **Upstash Redis is the guardrails state layer.**
  - Rate-limit counters
  - Dedup windows
  - Ephemeral safety controls (not the system of record)

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
| `POST /api/auth/*` | Scaffolded / planned | Production auth still staged |
| `GET /api/workspace` | Scaffolded / placeholder | Staged module route |
| `GET /api/profile` | Scaffolded / placeholder | Staged module route |

---

## Local Development Setup

### Prerequisites

- Node.js 22.x recommended (backend target)
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

- Never commit real secrets.
- Keep only template/example env files in version control.

---

## Repository Scope and Delivery Standard

### `verum_FE` owns

- Marketing and product route UX
- Query page rendering and state semantics
- Typed client integration with backend contracts
- Demo/staged auth entry flow (current phase)

### `verum_BE` owns

- Query orchestration and retrieval pipeline
- Grounding, synthesis, and citations
- Supabase/PostgreSQL persistence and retrieval logic
- Upstash guardrails behavior
- Runtime readiness/prewarm controls

Delivery standard for current phase:

- clear module boundaries
- explicit status semantics
- source-backed outputs
- no fake parity claims for non-operational modules
- incremental expansion from Module 1 into remaining jurisdictions/modules
