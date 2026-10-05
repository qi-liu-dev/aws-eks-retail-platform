# Progress
- Upstream pinned at: v1.6.3
- Current phase: 1 (local Docker)
- Done: repository setup
- Next: run with Docker Compose, write docs/services.md

## Learning notes

- 2026-10-05, memory sizing: Codex's initial planning estimate was 3-5 GiB for
  the containers, or 5-7 GiB including Docker VM overhead and startup headroom.
  One `docker stats` snapshot, about nine minutes after startup and after one
  order, totaled 2,345.5 MiB (about 2.29 GiB) across all 11 containers, below
  the estimated container range. This is one observed workload sample, not a
  measurement of startup peaks or total Docker VM memory use.
