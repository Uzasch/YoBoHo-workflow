---
project_name: 'yoboho-workflow'
user_name: 'Uzair'
date: '2026-01-12'
sections_completed: ['technology_stack', 'language_rules', 'framework_rules', 'testing_rules', 'code_quality', 'workflow_rules', 'critical_rules']
status: 'complete'
rule_count: 65
optimized_for_llm: true
---

# Project Context for AI Agents

_This file contains critical rules and patterns that AI agents must follow when implementing code in this project. Focus on unobvious details that agents might otherwise miss._

---

## Technology Stack & Versions

### Core Stack
- **Next.js 15** - App Router only (no Pages Router)
- **React 19** - Server Components by default
- **TypeScript** - Strict mode enabled
- **Tailwind CSS** - Utility-first styling
- **Node.js 20+** - LTS version

### Database & Auth
- **Supabase** - PostgreSQL database
- **@supabase/supabase-js** - Client SDK
- **@supabase/ssr** - Server-side auth
- **RLS** - Row Level Security enforced

### Key Dependencies
- **@google/genai** - Gemini AI integration
- **shadcn/ui** - Accessible component primitives
- **Zod** - Runtime validation
- **React Hook Form** - Form state management

---

## Language-Specific Rules (TypeScript)

### Configuration
- Strict mode enabled - no `any` types without explicit justification
- Path aliases: `@/` maps to `src/`
- ESM imports only - no CommonJS `require()`

### Import/Export Patterns
- Named exports for utilities, types, and hooks
- Default exports ONLY for page/layout components
- Import order: React → External packages → Internal modules → Types → Styles

### Type Patterns
- Use `interface` for object shapes, `type` for unions/intersections
- Zod schemas are source of truth - derive types with `z.infer<typeof schema>`
- Database types generated from Supabase - never manually define

### Case Transformation
- Database uses `snake_case` - API/code uses `camelCase`
- Transform at the data layer boundary (`lib/utils/transformCase.ts`)
- Never mix cases in the same context

### Error Handling
- Server Actions: Return `{ data, error }` objects - NEVER throw
- Route Handlers: Use proper HTTP status codes
- Client: Catch errors, display `error.message`, log full error

---

## Framework-Specific Rules (Next.js 15 / React 19)

### Server vs Client Components
- **Default to Server Components** - only add `'use client'` when needed
- Client components needed for: hooks, event handlers, browser APIs
- Keep client components small - push logic to server where possible

### Data Fetching
- Server Components fetch data directly (no useEffect)
- Use `async/await` in Server Components
- NO client-side data fetching libraries (no SWR, React Query)

### Server Actions vs Route Handlers
- **Server Actions** (`actions/*.ts`): All mutations (create, update, delete)
- **Route Handlers** (`api/`): External integrations, webhooks, AI queries
- Never use Route Handlers for internal CRUD operations

### Routing Patterns
- Route groups: `(auth)`, `(dashboard)` for layout separation
- Dynamic routes: `[id]` for single resources
- Loading states: `loading.tsx` files with Suspense
- Error boundaries: `error.tsx` files per route segment

### State Management
- Server state: Server Components + props drilling
- Client state: React Context for auth/theme only
- Form state: React Hook Form (never useState for forms)
- URL state: `useSearchParams` for filters/pagination

### Supabase Client Usage
- `lib/supabase/client.ts` - Browser only (Client Components)
- `lib/supabase/server.ts` - Server Components, Server Actions
- `lib/supabase/admin.ts` - Service role (migrations, seeding only)
- NEVER import browser client in server code

---

## Testing Rules

### Test Organization
- Co-located tests: `TaskCard.test.tsx` next to `TaskCard.tsx`
- E2E tests: `tests/e2e/*.spec.ts`
- Test utilities: `tests/setup.ts`, `tests/mocks/`

### Test Structure
- Use `describe` blocks for grouping related tests
- Test names: "should [expected behavior] when [condition]"
- Arrange-Act-Assert pattern in all tests

### What to Test
- Server Actions: Test business logic and error cases
- Components: Test user interactions and rendered output
- Utilities: Test edge cases and transformations
- E2E: Test critical user flows (auth, task creation, workflow)

### What NOT to Test
- shadcn/ui components (already tested)
- Supabase client internals
- Next.js framework behavior
- Pure type definitions

### Mocking
- Mock Supabase client in unit tests (`tests/mocks/supabase.ts`)
- Never mock in E2E tests - use test database
- Mock external APIs (YouTube, GCS) at Route Handler level

### Coverage Expectations
- Server Actions: 80%+ coverage
- Utility functions: 90%+ coverage
- Components: Focus on behavior, not implementation

---

## Code Quality & Style Rules

### Naming Conventions

| Context | Convention | Example |
|---------|------------|---------|
| Database tables | snake_case, plural | `tasks`, `workflow_events` |
| Database columns | snake_case | `created_at`, `user_id` |
| API routes | kebab-case | `/api/ai/query` |
| Components | PascalCase | `TaskCard.tsx` |
| Utilities | camelCase | `formatDate.ts` |
| Constants | SCREAMING_SNAKE | `MAX_RETRY_COUNT` |
| Types/Interfaces | PascalCase | `Task`, `WorkflowEvent` |

### File Organization
- Components: `components/features/{domain}/` or `components/ui/`
- No barrel files (`index.ts`) - import directly from source
- One component per file (exception: tightly coupled sub-components)

### Code Style
- Prefer `const` over `let`, never use `var`
- Use early returns to reduce nesting
- Destructure props and objects at function start
- No magic numbers - use named constants

### Documentation
- NO JSDoc for obvious functions
- Comments only for "why", not "what"
- README files only at project root and major feature directories

### API Response Format
```typescript
// Always use this structure
type ApiResponse<T> =
  | { data: T; error: null }
  | { data: null; error: { message: string; code: string } }
```

### Error Codes
`AUTH_ERROR` | `NOT_FOUND` | `VALIDATION_ERROR` | `SERVER_ERROR` | `INTEGRATION_ERROR`

---

## Development Workflow Rules

### Git Conventions
- Branch naming: `feature/`, `fix/`, `chore/` prefixes
- Commit messages: Conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- Keep commits atomic - one logical change per commit

### Environment Variables
- `.env.local` - Local development (never commit)
- `.env.example` - Template with placeholder values (commit this)
- Prefix client-exposed vars with `NEXT_PUBLIC_`
- Server-only secrets: `SUPABASE_SERVICE_ROLE_KEY`, `GOOGLE_AI_API_KEY`

### Database Migrations
- Use Supabase CLI: `supabase migration new {name}`
- Migration naming: `00001_descriptive_name.sql`
- Always include rollback comments in migrations
- Test migrations locally before applying to production

### CI/CD Pipeline
- GitHub Actions for: lint, type-check, test
- Vercel for: preview deploys (PR), production deploy (main)
- All checks must pass before merge

### Local Development
- `npm run dev` - Start Next.js dev server
- `supabase start` - Start local Supabase
- `supabase db reset` - Reset local DB with migrations + seed

### Event Logging (Critical)
- ALL state changes must create an event record
- Event format: `{entity}.{action}` (e.g., `task.created`)
- Events power AI queries - incomplete logging breaks AI features

---

## Critical Don't-Miss Rules

### Anti-Patterns to AVOID

**Database:**
- NEVER bypass RLS with service role in application code
- NEVER store user passwords (Supabase Auth handles this)
- NEVER use `SELECT *` - always specify columns

**Server Actions:**
- NEVER throw errors - always return `{ data, error }`
- NEVER call Server Actions from Route Handlers
- NEVER use `redirect()` inside try/catch blocks

**Components:**
- NEVER use `useEffect` for data fetching (use Server Components)
- NEVER put `'use client'` at top of files that don't need it
- NEVER import from `lib/supabase/client.ts` in Server Components

**Security:**
- NEVER expose `SUPABASE_SERVICE_ROLE_KEY` to client
- NEVER trust client-side auth checks alone (RLS is the gate)
- NEVER log passwords, tokens, or API keys

### Edge Cases to Handle

- Empty states: Always show meaningful UI when no data exists
- Loading states: Every async operation needs a loading indicator
- Error boundaries: Catch and display errors gracefully per route
- Optimistic updates: Show immediate feedback, handle rollback on failure

### Project-Specific Rules

- **IP Isolation**: All queries must filter by user's assigned IPs (except leadership roles)
- **Event Logging**: Every mutation must create a corresponding event - no exceptions
- **Graceful Degradation**: YouTube/GCS failures must not break core workflow operations
- **AI Query Safety**: Never execute raw SQL from AI - always use parameterized queries

---

## Usage Guidelines

**For AI Agents:**
- Read this file before implementing any code
- Follow ALL rules exactly as documented
- When in doubt, prefer the more restrictive option
- Update this file if new patterns emerge

**For Humans:**
- Keep this file lean and focused on agent needs
- Update when technology stack changes
- Review quarterly for outdated rules
- Remove rules that become obvious over time

---

_Last Updated: 2026-01-12_

