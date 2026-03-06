---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
inputDocuments:
  - "planning-artifacts/product-brief-yoboho-workflow-2026-01-08.md"
  - "planning-artifacts/prd.md"
workflowType: 'architecture'
project_name: 'yoboho-workflow'
user_name: 'Uzair'
date: '2026-01-12'
status: 'complete'
completedAt: '2026-01-12'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**
58 requirements across 9 categories covering: personal queue dashboards, visual workflow canvas, task management with event logging, Notion-style table views, RBAC user management, AI natural language queries, email notifications, YouTube/GCS integrations, and Gantt-based reporting.

**Non-Functional Requirements:**
- Performance: Page load <2s, AI query <30s
- Reliability: 100% data accuracy (non-negotiable), 99% availability during business hours
- Security: RBAC with IP-level tenant isolation, session management
- Scale: 50 concurrent users, designed for internal team

**Scale & Complexity:**
- Primary domain: Internal productivity/workflow web application
- Complexity level: Medium
- Estimated architectural components: 7-9 major subsystems

### Technical Constraints & Dependencies

- Internal tool only (no external SaaS considerations)
- Desktop-first design (9-5 production hours)
- Must integrate with existing YouTube API and Google Cloud Bucket
- Event-driven data layer is foundational, not optional
- No UX spec available - UI decisions require extra architectural attention
- **No real-time push updates required** - standard request/response with refresh is sufficient

### Cross-Cutting Concerns Identified

1. **Event Logging** - All task state changes must be captured for AI queryability
2. **RBAC Enforcement** - IP+Workflow assignment model affects all data access
3. **Tenant Isolation** - IP-level data separation with cross-IP reporting for leadership
4. **Graceful Degradation** - External integrations must not block core workflow operations

## Starter Template Evaluation

### Primary Technology Domain

Full-stack internal web application based on project requirements analysis.

### Technical Preferences

- **Language:** TypeScript
- **Framework:** Next.js 15 (App Router)
- **Styling:** Tailwind CSS
- **Database:** Supabase (PostgreSQL)
- **Auth:** Supabase Auth
- **Deployment:** Vercel (primary), Docker (containerization)

### Selected Starter Approach

**Approach:** Clean Next.js baseline + Supabase integration

**Rationale:**
- create-next-app provides minimal, up-to-date foundation
- Supabase packages added separately for latest versions
- Avoids opinionated boilerplate that may conflict with project needs
- Maximum control over architecture decisions

**Initialization Commands:**

```bash
npx create-next-app@latest yoboho-workflow --typescript --tailwind --eslint --app --src-dir --turbopack
npm install @supabase/supabase-js @supabase/ssr
```

### Architectural Decisions Established

| Layer | Decision |
|-------|----------|
| **Runtime** | Node.js with TypeScript |
| **Frontend** | React 19 via Next.js 15 App Router |
| **Styling** | Tailwind CSS utility classes |
| **Database** | PostgreSQL via Supabase |
| **Auth** | Supabase Auth with @supabase/ssr for server-side |
| **API Layer** | Next.js Route Handlers + Supabase client |
| **Build Tool** | Turbopack (dev), Next.js compiler (prod) |

**Note:** Project initialization should be the first implementation story.

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**
- Database: Supabase (PostgreSQL)
- Auth: Supabase Auth with RLS
- API Pattern: Server Actions + Route Handlers
- AI Layer: Google AI (Gemini)

**Important Decisions (Shape Architecture):**
- Component Library: shadcn/ui
- Form Handling: React Hook Form + Zod
- State: React Context + Server Components

**Deferred Decisions (Post-MVP):**
- Caching layer (add if performance requires)
- Advanced monitoring (LogRocket, etc.)

### Data Architecture

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **Validation** | Zod | TypeScript-first, integrates with Server Actions |
| **Migrations** | Supabase CLI | Native to database, single ecosystem |
| **Caching** | None (MVP) | 50 users, refresh model, revisit if needed |

### Authentication & Security

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **RBAC** | Supabase RLS | Database-enforced, can't be bypassed |
| **API Security** | Supabase JWT | Native to auth system, validate in Route Handlers |
| **Session** | Supabase Auth cookies via @supabase/ssr | Server-side session handling |

### API & Communication Patterns

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **Mutations** | Next.js Server Actions | Colocated, type-safe, simple |
| **Integrations** | Next.js Route Handlers | YouTube API, GCS, external calls |
| **AI Queries** | Google AI (Gemini) via @google/genai | Server-side, production queries |

**AI Query Implementation Note:**
- Use Route Handler for AI queries (keeps API key server-side)
- Parse natural language → SQL query → return formatted response
- Leverage Supabase's PostgreSQL for complex production queries

### Frontend Architecture

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **State** | React Context + Server Components | Minimal client state with App Router |
| **Components** | shadcn/ui | Tailwind-native, full control, accessible |
| **Forms** | React Hook Form + Zod | Performant, validates with same schema |
| **Styling** | Tailwind CSS | Already decided in starter |

### Infrastructure & Deployment

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **Hosting** | Vercel | Zero-config Next.js, edge functions |
| **CI/CD** | Vercel (deploys) + GitHub Actions (tests) | Separation of concerns |
| **Monitoring** | Vercel Analytics + Sentry | Free tier sufficient, error tracking |
| **Containers** | Docker | Local dev parity, optional self-hosting |

### Decision Impact Analysis

**Implementation Sequence:**
1. Project init (Next.js + Supabase packages)
2. Supabase project setup + initial schema
3. Auth flow with RLS policies
4. Core UI components (shadcn/ui setup)
5. Workflow engine + task management
6. AI query layer integration

**Cross-Component Dependencies:**
- RLS policies depend on auth being complete
- AI queries depend on event logging schema
- Forms depend on Zod schemas matching database types

## Implementation Patterns & Consistency Rules

### Naming Patterns

**Database (Supabase/PostgreSQL):**
| Element | Convention | Example |
|---------|------------|---------|
| Tables | snake_case, plural | `tasks`, `workflow_events` |
| Columns | snake_case | `created_at`, `user_id` |
| Foreign keys | `{table}_id` | `workflow_id`, `ip_id` |
| Indexes | `idx_{table}_{column}` | `idx_tasks_status` |

**API (Next.js Route Handlers):**
| Element | Convention | Example |
|---------|------------|---------|
| Routes | kebab-case, plural | `/api/workflows`, `/api/tasks` |
| Route params | `[id]` | `/api/tasks/[id]` |
| Query params | camelCase | `?ipId=123&status=active` |

**Code (TypeScript/React):**
| Element | Convention | Example |
|---------|------------|---------|
| Components | PascalCase | `TaskCard.tsx` |
| Functions | camelCase | `getTaskById()` |
| Variables | camelCase | `currentTask` |
| Constants | SCREAMING_SNAKE | `MAX_RETRY_COUNT` |
| Types/Interfaces | PascalCase | `Task`, `WorkflowEvent` |
| Files (components) | PascalCase | `TaskCard.tsx` |
| Files (utilities) | camelCase | `formatDate.ts` |

### Structure Patterns

**Project Organization:**
```
src/
├── app/                    # Next.js App Router
│   ├── (auth)/            # Auth route group
│   ├── (dashboard)/       # Dashboard route group
│   ├── api/               # Route Handlers
│   └── layout.tsx
├── components/
│   ├── ui/                # shadcn/ui components
│   └── features/          # Feature-specific components
├── lib/
│   ├── supabase/          # Supabase clients
│   ├── validations/       # Zod schemas
│   └── utils/             # Utilities
├── types/                 # TypeScript types
└── actions/               # Server Actions
```

**Test Location:** Co-located (`TaskCard.test.tsx` next to `TaskCard.tsx`)

### Format Patterns

**API Response Structure:**
```typescript
// Success
{ data: T, error: null }

// Error
{ data: null, error: { message: string, code: string } }
```

**Error Codes:** `AUTH_ERROR`, `NOT_FOUND`, `VALIDATION_ERROR`, `SERVER_ERROR`

**Dates:** ISO 8601 in API, formatted for display in UI

**JSON Fields:** camelCase in responses (transform from snake_case DB)

### Communication Patterns

**Event Naming:** `{entity}.{action}` (e.g., `task.created`, `task.status_changed`)

**Event Payload:**
```typescript
{
  event_type: string,
  entity_id: string,
  entity_type: string,
  user_id: string,
  timestamp: string,
  metadata: object
}
```

### Process Patterns

**Error Handling:**
- Server Actions: Return `{ data, error }` - never throw
- Route Handlers: Return proper HTTP status codes
- Client: Display `error.message`, log full error to Sentry

**Loading States:**
- Route-level: React Suspense + `loading.tsx`
- Mutations: `isPending` from `useTransition`
- Naming: `isLoading`, `isPending`, `isSubmitting`

**Auth Flow:**
- Middleware checks Supabase session
- Unauthenticated → redirect to `/login`
- RLS handles data-level authorization

### Logging Patterns

**Log Levels:**
| Level | Use Case |
|-------|----------|
| `error` | Unexpected failures, exceptions |
| `warn` | Recoverable issues, degraded state |
| `info` | Business events, key actions |
| `debug` | Development troubleshooting |

**Log Format:**
```typescript
{
  level: string,
  message: string,
  timestamp: string,
  context: { userId?, requestId?, action?, metadata? }
}
```

**Destinations:**
- Development: Console (pretty-printed)
- Production: Vercel logs (JSON) + Sentry (errors)

**What to Log:** Server Actions, Route Handlers, auth events, business events, integration calls, errors with stack traces

**What NOT to Log:** Passwords, tokens, API keys, PII (use user IDs instead)

**Implementation:** Simple console wrapper utility (`lib/logger.ts`)

### Enforcement Guidelines

**All AI Agents MUST:**
- Follow naming conventions exactly as specified
- Use the defined API response structure for all endpoints
- Log using the standard logger utility
- Place files in the correct directory structure
- Use co-located tests

**Anti-Patterns to Avoid:**
- Mixing snake_case and camelCase in same context
- Throwing errors from Server Actions
- Logging sensitive data
- Creating new folders outside defined structure
- Using different date formats

## Project Structure & Boundaries

### Complete Project Directory Structure

```
yoboho-workflow/
├── README.md
├── package.json
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── components.json                 # shadcn/ui config
├── .env.local
├── .env.example
├── .gitignore
├── Dockerfile
├── docker-compose.yml
│
├── .github/
│   └── workflows/
│       ├── ci.yml                  # Lint, type-check, test
│       └── deploy.yml              # Vercel deployment (optional)
│
├── supabase/
│   ├── config.toml
│   ├── seed.sql
│   └── migrations/
│       ├── 00001_initial_schema.sql
│       ├── 00002_rls_policies.sql
│       └── ...
│
├── public/
│   └── assets/
│       └── icons/
│
├── src/
│   ├── app/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   ├── loading.tsx
│   │   ├── error.tsx
│   │   ├── not-found.tsx
│   │   │
│   │   ├── (auth)/
│   │   │   ├── layout.tsx
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   └── callback/
│   │   │       └── route.ts        # Supabase auth callback
│   │   │
│   │   ├── (dashboard)/
│   │   │   ├── layout.tsx          # Sidebar, header
│   │   │   ├── page.tsx            # Dashboard home (My Work)
│   │   │   ├── loading.tsx
│   │   │   │
│   │   │   ├── tasks/
│   │   │   │   ├── page.tsx        # Task list views
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx    # Task detail
│   │   │   │
│   │   │   ├── workflows/
│   │   │   │   ├── page.tsx        # Workflow list
│   │   │   │   ├── [id]/
│   │   │   │   │   ├── page.tsx    # Workflow detail
│   │   │   │   │   └── canvas/
│   │   │   │   │       └── page.tsx # Canvas editor
│   │   │   │   └── new/
│   │   │   │       └── page.tsx    # Create workflow
│   │   │   │
│   │   │   ├── ips/
│   │   │   │   ├── page.tsx        # IP (channel) list
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx    # IP detail + workflows
│   │   │   │
│   │   │   ├── observatory/
│   │   │   │   └── page.tsx        # Process Observatory view
│   │   │   │
│   │   │   ├── upload-ready/
│   │   │   │   └── page.tsx        # Channel Manager dashboard
│   │   │   │
│   │   │   ├── ai/
│   │   │   │   └── page.tsx        # AI query interface
│   │   │   │
│   │   │   └── settings/
│   │   │       ├── page.tsx
│   │   │       └── users/
│   │   │           └── page.tsx    # User management (admin)
│   │   │
│   │   └── api/
│   │       ├── ai/
│   │       │   └── query/
│   │       │       └── route.ts    # AI query endpoint
│   │       ├── integrations/
│   │       │   ├── youtube/
│   │       │   │   └── route.ts
│   │       │   └── gcs/
│   │       │       └── route.ts
│   │       └── webhooks/
│   │           └── route.ts
│   │
│   ├── actions/
│   │   ├── tasks.ts                # Task mutations
│   │   ├── workflows.ts            # Workflow mutations
│   │   ├── users.ts                # User mutations
│   │   └── ips.ts                  # IP mutations
│   │
│   ├── components/
│   │   ├── ui/                     # shadcn/ui components
│   │   │   ├── button.tsx
│   │   │   ├── card.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── dropdown-menu.tsx
│   │   │   ├── form.tsx
│   │   │   ├── input.tsx
│   │   │   ├── select.tsx
│   │   │   ├── table.tsx
│   │   │   ├── tabs.tsx
│   │   │   └── ...
│   │   │
│   │   ├── layout/
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Header.tsx
│   │   │   ├── NavItem.tsx
│   │   │   └── UserMenu.tsx
│   │   │
│   │   └── features/
│   │       ├── tasks/
│   │       │   ├── TaskCard.tsx
│   │       │   ├── TaskList.tsx
│   │       │   ├── TaskBoard.tsx
│   │       │   ├── TaskGallery.tsx
│   │       │   ├── TaskStatusBadge.tsx
│   │       │   ├── TaskForm.tsx
│   │       │   └── TaskCard.test.tsx
│   │       │
│   │       ├── workflows/
│   │       │   ├── WorkflowCard.tsx
│   │       │   ├── WorkflowList.tsx
│   │       │   ├── ProcessNode.tsx
│   │       │   ├── Canvas.tsx
│   │       │   ├── CanvasToolbar.tsx
│   │       │   ├── DependencyLine.tsx
│   │       │   └── GanttPreview.tsx
│   │       │
│   │       ├── dashboard/
│   │       │   ├── QueueView.tsx
│   │       │   ├── ViewToggle.tsx
│   │       │   └── StatsCard.tsx
│   │       │
│   │       ├── ai/
│   │       │   ├── QueryInput.tsx
│   │       │   ├── QueryResult.tsx
│   │       │   └── QueryHistory.tsx
│   │       │
│   │       └── users/
│   │           ├── UserList.tsx
│   │           ├── UserForm.tsx
│   │           └── RoleSelector.tsx
│   │
│   ├── lib/
│   │   ├── supabase/
│   │   │   ├── client.ts           # Browser client
│   │   │   ├── server.ts           # Server client
│   │   │   ├── middleware.ts       # Auth middleware helper
│   │   │   └── admin.ts            # Service role client
│   │   │
│   │   ├── validations/
│   │   │   ├── task.ts             # Task Zod schemas
│   │   │   ├── workflow.ts
│   │   │   ├── user.ts
│   │   │   └── ip.ts
│   │   │
│   │   ├── utils/
│   │   │   ├── formatDate.ts
│   │   │   ├── transformCase.ts    # snake_case <-> camelCase
│   │   │   └── cn.ts               # Tailwind classnames
│   │   │
│   │   ├── logger.ts               # Console wrapper
│   │   ├── constants.ts
│   │   └── ai.ts                   # Google AI client setup
│   │
│   ├── types/
│   │   ├── database.ts             # Generated from Supabase
│   │   ├── task.ts
│   │   ├── workflow.ts
│   │   ├── user.ts
│   │   ├── ip.ts
│   │   └── event.ts
│   │
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useTasks.ts
│   │   └── useWorkflows.ts
│   │
│   └── middleware.ts               # Auth + RLS enforcement
│
└── tests/
    ├── setup.ts
    ├── mocks/
    │   └── supabase.ts
    └── e2e/
        ├── auth.spec.ts
        └── tasks.spec.ts
```

### Architectural Boundaries

**API Boundaries:**
| Boundary | Enforcement |
|----------|-------------|
| External APIs | Route Handlers only (`/api/integrations/`) |
| Internal mutations | Server Actions (`/actions/`) |
| Auth | Middleware + Supabase RLS |
| Data access | Only via `lib/supabase/` clients |

**Component Boundaries:**
| Layer | Communication |
|-------|---------------|
| Pages → Components | Props (Server Components pass data down) |
| Components → Actions | Direct import and call |
| Components → Hooks | Client components only |

**Data Boundaries:**
| Source | Access Pattern |
|--------|----------------|
| Database | Supabase client with RLS |
| External APIs | Route Handlers with error handling |
| File storage | GCS via Route Handler |

### Requirements to Structure Mapping

| FR Category | Primary Location |
|-------------|------------------|
| **Dashboard & Queue (FR1-8)** | `app/(dashboard)/page.tsx`, `components/features/dashboard/`, `components/features/tasks/` |
| **Workflow Canvas (FR9-20)** | `app/(dashboard)/workflows/[id]/canvas/`, `components/features/workflows/` |
| **Task Management (FR21-28)** | `app/(dashboard)/tasks/`, `actions/tasks.ts`, `components/features/tasks/` |
| **Workflow Table View (FR29-35)** | `components/features/tasks/TaskList.tsx`, `TaskBoard.tsx`, `TaskGallery.tsx` |
| **User Management (FR36-41)** | `app/(dashboard)/settings/users/`, `actions/users.ts`, `components/features/users/` |
| **AI Query Layer (FR42-47)** | `app/(dashboard)/ai/`, `app/api/ai/query/`, `lib/ai.ts`, `components/features/ai/` |
| **Notifications (FR48-51)** | Supabase Edge Functions or external email service |
| **Integrations (FR52-54)** | `app/api/integrations/youtube/`, `app/api/integrations/gcs/` |
| **Reporting (FR55-58)** | `components/features/workflows/GanttPreview.tsx`, `app/(dashboard)/observatory/` |

### Data Flow

**Standard Request Flow:**
```
User Action → Server Action → Supabase (RLS enforced) → Event Log → Response
                    ↓
              Log to logger.ts
```

**AI Query Flow:**
```
User Query → Route Handler → Google AI → Generate SQL → Supabase Query → Format Response
```

**Integration Flow:**
```
Trigger → Route Handler → External API → Transform Response → Return to Client
              ↓
        Graceful degradation on failure
```

## Architecture Validation Results

### Coherence Validation ✅

**Decision Compatibility:** All technology choices (Next.js 15, Supabase, Tailwind, shadcn/ui, Google AI) work together without conflicts. Stack is widely used and well-documented.

**Pattern Consistency:** Implementation patterns align with technology conventions. Naming follows community standards for each layer.

**Structure Alignment:** Project structure follows Next.js App Router conventions and supports all architectural decisions.

### Requirements Coverage ✅

**Functional Requirements:** All 58 FRs across 9 categories are mapped to specific locations in the project structure.

**Non-Functional Requirements:**
- Performance: Server Components + minimal client JS ensures <2s load
- Security: Supabase RLS enforces RBAC at database level
- Reliability: Event logging captures all state changes for audit
- Scale: Architecture supports 50 concurrent users comfortably

### Implementation Readiness ✅

**Decision Completeness:** All critical decisions documented with versions and rationale.

**Structure Completeness:** Complete directory tree with all files specified.

**Pattern Completeness:** Comprehensive patterns for naming, structure, format, communication, and process.

### Gap Analysis

**No Critical Gaps** - Architecture is ready for implementation.

**Minor Gaps (resolve during implementation):**
- Canvas library for workflow builder (recommend @xyflow/react)
- Email notification service (recommend Resend or Supabase Edge Functions)
- Testing framework configuration (standard Jest + RTL)

### Architecture Completeness Checklist

**Requirements Analysis**
- [x] Project context analyzed
- [x] Scale and complexity assessed
- [x] Technical constraints identified
- [x] Cross-cutting concerns mapped

**Architectural Decisions**
- [x] Critical decisions documented
- [x] Technology stack specified
- [x] Integration patterns defined
- [x] Performance considerations addressed

**Implementation Patterns**
- [x] Naming conventions established
- [x] Structure patterns defined
- [x] Communication patterns specified
- [x] Process patterns documented

**Project Structure**
- [x] Complete directory structure defined
- [x] Component boundaries established
- [x] Integration points mapped
- [x] Requirements mapping complete

### Architecture Readiness Assessment

**Overall Status:** READY FOR IMPLEMENTATION

**Confidence Level:** High

**Key Strengths:**
- Boring, proven technology stack
- Database-enforced security via RLS
- Event-driven architecture enables AI queries from day one
- Clear patterns prevent agent implementation conflicts

**First Implementation Priority:**
```bash
npx create-next-app@latest yoboho-workflow --typescript --tailwind --eslint --app --src-dir --turbopack
```

## Architecture Completion Summary

### Workflow Completion

**Architecture Decision Workflow:** COMPLETED
**Total Steps Completed:** 8
**Date Completed:** 2026-01-12
**Document Location:** planning-artifacts/architecture.md

### Final Architecture Deliverables

**Complete Architecture Document**
- All architectural decisions documented with specific versions
- Implementation patterns ensuring AI agent consistency
- Complete project structure with all files and directories
- Requirements to architecture mapping
- Validation confirming coherence and completeness

**Implementation Ready Foundation**
- 15+ architectural decisions made
- 6 pattern categories defined (naming, structure, format, communication, process, logging)
- 9 major architectural components specified
- 58 functional requirements fully supported

**AI Agent Implementation Guide**
- Technology stack with verified versions
- Consistency rules that prevent implementation conflicts
- Project structure with clear boundaries
- Integration patterns and communication standards

### Implementation Handoff

**For AI Agents:**
This architecture document is your complete guide for implementing yoboho-workflow. Follow all decisions, patterns, and structures exactly as documented.

**First Implementation Priority:**
```bash
npx create-next-app@latest yoboho-workflow --typescript --tailwind --eslint --app --src-dir --turbopack
npm install @supabase/supabase-js @supabase/ssr zod react-hook-form @google/genai
npx shadcn@latest init
```

**Development Sequence:**
1. Initialize project using documented starter template
2. Set up Supabase project and initial schema
3. Implement auth flow with RLS policies
4. Set up core UI components (shadcn/ui)
5. Build features following established patterns
6. Maintain consistency with documented rules

### Quality Assurance Checklist

**Architecture Coherence**
- [x] All decisions work together without conflicts
- [x] Technology choices are compatible
- [x] Patterns support the architectural decisions
- [x] Structure aligns with all choices

**Requirements Coverage**
- [x] All functional requirements are supported
- [x] All non-functional requirements are addressed
- [x] Cross-cutting concerns are handled
- [x] Integration points are defined

**Implementation Readiness**
- [x] Decisions are specific and actionable
- [x] Patterns prevent agent conflicts
- [x] Structure is complete and unambiguous
- [x] Examples are provided for clarity

---

**Architecture Status:** READY FOR IMPLEMENTATION

**Next Phase:** Begin implementation using the architectural decisions and patterns documented herein.

**Document Maintenance:** Update this architecture when major technical decisions are made during implementation.

