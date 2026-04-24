# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies. The project now includes a Todo List Frontend web app at the root preview path, backed by the user's existing Render backend through a local API proxy.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite + Tailwind CSS

## Artifacts

- `artifacts/api-server` — shared Express API server under `/api`.
- `artifacts/todo-list-frontend` — React Todo List frontend at `/`.
- `artifacts/mockup-sandbox` — canvas/component preview sandbox at `/__mockup`.

## Todo List Frontend

- Uses backend base path `/api/todolist/api` from the browser.
- `artifacts/api-server/src/routes/todolistProxy.ts` proxies `/api/todolist/*` to `https://todolist-backend-4q3m.onrender.com/*` to avoid browser CORS issues with the Render backend.
- Supports login, registration, email OTP verification, MFA OTP verification, password reset, profile loading, todo listing, search/filter, create, update status/title, and delete.
- Stores the access token in `localStorage` and attaches it as a Bearer token for protected backend requests.

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/todo-list-frontend run dev` — run Todo List frontend locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
