# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

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
- **Frontend**: React + Vite + TailwindCSS + shadcn/ui + framer-motion + wouter

## Artifacts

### DriveEZ DZ (`artifacts/drivez-dz`)
Algerian driving school platform (منصة تعليم السياقة الجزائرية).
- **Preview path**: `/` (root)
- **Features**: Bilingual AR/FR, quiz system, lessons, student progress tracking, dashboard
- **Theme**: Algeria-inspired (deep green + red accent)

### API Server (`artifacts/api-server`)
Shared Express 5 backend serving all frontend artifacts.
- **Preview path**: `/api`
- **Routes**: /questions, /lessons, /quizzes, /progress, /stats

## Database Schema

Tables in PostgreSQL:
- `questions` — Driving test questions (bilingual AR/FR)
- `lessons` — Driving lessons with content (bilingual)
- `quizzes` — Student quiz sessions with scores
- `progress` — Student progress tracking

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## Notes on Codegen

The codegen script fixes a known orval conflict where `api-zod/src/index.ts` exports both `./generated/api` (Zod schemas) and `./generated/types` (TS interfaces), causing duplicate name errors. The script overwrites the index.ts after codegen to only export from `./generated/api`.

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
