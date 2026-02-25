# ADR 0001: WSL filesystem + VS Code Remote - WSL + Dev Containers workflow

## Status
Accepted

## Context
Apex Ledger is a long-term portfolio project built on React, Vite, and TypeScript using WSL2 and Docker/Dev Containers.
The development environment spans Windows (host) and Linux (WSL2). Mixed filesystems and toolchains can introduce:
- Slow Node installs/builds (I/O heavy)
- Unreliable file watching
- Line ending and permission issues
- Drift between local dev and Linux CI environments

## Decision
- Store the repository inside the WSL Linux filesystem under:
  - /home/jpate/dev/personal/active/apex-ledger
- Open and develop the repo using VS Code **Remote - WSL**
- Use **Dev Containers** (.devcontainer/devcontainer.json) for consistent tooling
- Use Docker running in WSL2 (preferred) or Docker Desktop with WSL2 integration

## Rationale
- Best I/O performance for Node/TypeScript installs and builds when the repo is on the WSL filesystem
- Reliable Linux file watching behavior compared to /mnt/c
- Correct POSIX permissions and symlink behavior for scripts and tooling
- Better parity with Linux-based CI and production environments

## Alternatives Considered
1. Repo on Windows filesystem (C:\ or /mnt/c) + Dev Containers
   - Rejected due to slower I/O and file watcher issues for Node-heavy workloads
2. Developing fully on Windows without WSL
   - Rejected due to reduced parity with Linux-based containers/CI and more environment drift

## Consequences
- Developers must use Remote - WSL for best results
- Git line endings should be normalized to LF to prevent cross-OS issues
- Container/tooling configuration will be kept in-repo to support reproducibility
