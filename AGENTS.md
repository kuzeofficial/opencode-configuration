# Personal Rules

## Core Philosophy

Simplicity and readability above all. Every line must earn its place.
Prefer concise implementations, clean interfaces, and elegant solutions over brute-force approaches.
Never over-engineer. Never under-engineer. Match the architecture to the problem's complexity.

## AI Behavior

- Read and match existing codebase patterns before writing anything new
- If a util, helper, or component already exists in the project, use it
- Never leave TODOs, stubs, or placeholder code — implement fully or ask
- When unsure about a design decision, ask — never assume
- Propose the approach before making large refactors or architectural changes
- Write tests alongside every feature (TDD: test first, then implement)
- Keep responses concise and direct — no over-explaining obvious things
- Comments are almost never needed — code must be self-documenting
- The only acceptable comment explains *why*, never *what*
- Never create unnecessary files — consolidate when fewer files are clearer
- Never use generic catch-all error handling (no `catch (e) { console.error(e) }`)

## Language & Communication

- All code, comments, commits, and documentation in English
- Commit messages: conventional + atomic (`feat:`, `fix:`, `refactor:`, `test:`, `chore:`)
- One logical change per commit

## Code Style (All Languages)

- Write idiomatic code per language — Go like a Go dev, TS like a TS dev, Rust like a Rust dev
- Early returns and guard clauses always — avoid deep nesting
- Single responsibility per function and file — size follows naturally
- Constants and enums over magic strings and numbers
- Never ignore errors — handle or propagate with context
- Never leave `console.log` or debug prints in production code
- Flatten async flows — no nested callbacks or promise chains
- Let auto-formatters handle import ordering and formatting

## TypeScript / JavaScript

- Runtime: Bun
- Strict mode always — `strict: true`, no `any`, no implicit returns
- Formatter/linter: Biome
- Styling: Tailwind CSS + component libraries (shadcn/ui, BaseUI, Radix)
- State management: Zustand (React), Pinia (Vue)
- Server state: React Query (TanStack Query) — prefer over framework-native fetching
- Types are domain-driven: live in the domain layer, shared across features
- Never use `any` — prefer `unknown` + type narrowing when the type is unclear

## React / Next.js

- Composition over prop-drilling — compose small focused components
- Extract logic into custom hooks — components stay thin and declarative
- Smart (container) + Dumb (presentational) separation when it aids clarity

## Vue / Nuxt

- Extract logic into composables — components stay thin
- Composition API only — no Options API
- Pinia for client state, TanStack Query / useFetch for server state

## AdonisJS

- Follow AdonisJS v6 conventions (controllers, validators, middleware)
- Lucid ORM for database access — respect repository pattern on top
- Use AdonisJS built-in tooling (Vine validation, auth, mailer) before adding external packages

## Go

- Linter: golangci-lint, formatter: gofmt
- Accept interfaces, return structs (as a heuristic, not a dogma)
- Small interfaces (1-2 methods), compose upward
- Errors as values — always handle, wrap with context (`fmt.Errorf("...: %w", err)`)
- Propagate `context.Context` through call chains, never abuse `context.Value()`
- Table-driven tests as the default test pattern
- Functional options (`WithX()`) for library APIs only — config structs for internal code

## Python

- Linter/formatter: Ruff
- Type hints on all function signatures
- Follow PEP 8 and language idioms

## Rust

- Formatter: rustfmt, linter: clippy
- Use `Result<T, E>` and `Option<T>` — propagate errors with `?`
- Prefer ownership and borrowing clarity over lifetime gymnastics

## Architecture & Patterns

- New high-complexity projects: DDD (entities, value objects, aggregates, repositories)
- Existing projects: follow whatever conventions are already established
- Common pattern: Clean Architecture or Hexagonal — domain at the center
- Simple CRUD projects: handler → service → repository is sufficient
- Repository pattern always — abstract database access behind interfaces
- ORM always (Drizzle, Prisma, GORM, SQLAlchemy, Lucid) — never write raw SQL
- API design: REST for public, gRPC for internal services, tRPC for full-stack TS apps

## Project Structure

- Never flat — always organized into meaningful directories
- Monorepo with workspaces when building from scratch
- Feature/domain folders or type-based folders depending on project scope
- Environment config: follow framework conventions (no custom dotenv wrappers)

## Auth

- Prefer established libraries: Better Auth, Auth.js
- Choose auth strategy (JWT, sessions, OAuth) based on project requirements

## Logging & Observability

- If the project has observability infrastructure: full stack (logs + metrics + traces)
- Otherwise: minimal logging — errors and key events only
- Use the framework's built-in logger — no custom logging wrappers
- Structured logging (JSON with fields) when the framework supports it

## Dependencies

- Use proven, battle-tested packages — don't reinvent what's solved
- But don't add a dependency for something trivially implementable

## Prohibited Patterns

- `any` type in TypeScript
- God functions or god files
- Magic strings or numbers without constants
- Nested callback or promise chains
- Copy-paste duplication — extract and reuse
- Swallowed/ignored errors
- Business logic in controllers or handlers
- SQL queries outside the repository layer
- Leftover debug logging in committed code
- Comments that describe what the code does instead of why
- Mixing concerns — business logic in controllers or handlers
