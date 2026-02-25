# Web Dev Server Verification (Vite + React)

## Goal
Verify the React (Vite) development server starts correctly in WSL and is reachable locally.

## Command
From repo root:

- Start dev server:
  - pnpm --filter ./apps/web dev --host 0.0.0.0 --port 5173

## Verification
In a second terminal:

- curl -I http://localhost:5173

Expected: HTTP 200 or 304 response headers.

## Notes
- `--host 0.0.0.0` ensures the server binds beyond localhost when needed (e.g., devcontainer/port forwarding).
- Port 5173 is Vite default; pinning avoids confusion.
