# Apex Ledger

Enterprise-grade, full-stack ledger system built with modern TypeScript tooling.

## Overview

Apex Ledger is a modular monorepo designed to model a modern double-entry financial ledger.

It includes:

- React + Vite frontend
- NestJS backend
- PostgreSQL database
- Prisma ORM
- pnpm workspace monorepo
- Docker-based infrastructure
- Lightweight ADR documentation

---

## Architecture

Monorepo structure:

apps/
  web/        → React + Vite + TypeScript
  api/        → NestJS + Prisma
packages/
  domain/     → Pure TypeScript ledger logic (no framework dependencies)
infrastructure/
  compose/    → Docker Compose (PostgreSQL)
docs/
  decisions/  → Architecture Decision Records
  environment/→ Setup documentation

---

## Tech Stack

Frontend:
- React
- Vite
- TypeScript

Backend:
- NestJS
- Prisma
- PostgreSQL

Infrastructure:
- Docker
- WSL2
- pnpm workspaces

---

## Running Locally

### 1. Start Database

docker compose -f infrastructure/compose/docker-compose.yml up -d

### 2. Start API

pnpm --filter ./apps/api start:dev

### 3. Start Web

pnpm --filter ./apps/web dev --host 0.0.0.0 --port 5173

---

## Development Principles

- Strict TypeScript
- Domain logic isolated in `packages/domain`
- Double-entry accounting model
- Reproducible development environment
- ADR-driven architecture decisions

---

## Status

Active development.

