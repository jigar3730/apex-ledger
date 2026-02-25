# Apex Ledger – Environment Setup Guide

## Development Environment

- Host OS: Windows
- Linux Layer: WSL2
- Editor: VS Code (Remote - WSL)
- Package Manager: pnpm (via Corepack)
- Container Runtime: Docker (WSL2 integration)
- Database: PostgreSQL (Docker Compose)

---

## Repository Location

Stored inside WSL filesystem for performance:

/home/jpate/dev/personal/active/apex-ledger

Reason:
- Faster Node I/O
- Reliable file watching
- Linux parity with CI

---

## Package Manager Setup

Corepack enabled:

corepack enable
corepack prepare pnpm@latest --activate

Workspace root pins:

"packageManager": "pnpm@10.30.2"

---

## Monorepo Structure

apps/
  web/      → React + Vite + TypeScript
  api/      → NestJS + Prisma
packages/
  domain/   → Shared ledger logic (pure TypeScript)
infrastructure/
  compose/  → Docker Compose (Postgres)
docs/

---

## Running Services

### Web

pnpm --filter ./apps/web dev --host 0.0.0.0 --port 5173

Verify:
curl -I http://localhost:5173

### Database

docker compose -f infrastructure/compose/docker-compose.yml up -d

---

## Important Rules

- All business logic lives in packages/domain
- No money calculations inside React
- No direct DB access from web
- TypeScript strict mode will be enforced
- Environment variables are not committed
