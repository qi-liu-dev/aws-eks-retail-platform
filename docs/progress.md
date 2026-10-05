# Progress

- Upstream pinned at: v1.6.3
- Current phase: 2 (local Kubernetes with kind), not started
- Last updated: 2026-10-05

## Phase 1: local Docker (complete, 2026-10-05)
- Ran the v1.6.3 release Compose file locally: 11 containers
  (5 application services, 6 supporting services).
- Completed one full order in the browser
  (order ID 75e06b19-b201-435a-8ee5-27a8a5f680b2).
- Wrote docs/services.md: dependencies, ports, order flow, health checks,
  observed memory and operational findings.
- Spot-checked three claims in services.md against the Compose file:
  carts-db health check, UI port 8888, catalog depending on OpenSearch.
- Memory: about 2.3 GiB observed across all containers, against a planning
  estimate of 3 to 5 GiB. OpenSearch alone used 878 MiB (37%) with search disabled.

## Decisions
- 0001: separate application and platform repositories.

## Open issues
- The Compose stack is still running. Stop it before deploying the full app on kind.
- The Compose file is in /private/tmp. Move it to .local/.

## Next: Phase 2
- Create a kind cluster from a config file in this repo, deploy with the
  upstream Helm charts, complete an order, and practise kubectl troubleshooting.
- Decisions to make: pin the kind node image or not, run OpenSearch on kind
  or not, port-forward or Ingress for the UI.

## Gotchas
- After `brew install kubectl`, `which kubectl` still pointed to Docker
  Desktop's v1.32 copy because zsh had cached the old path. `rehash` fixed it.
  Version skew matters: kubectl should stay within one minor version of the cluster.