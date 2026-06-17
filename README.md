# microshift-homelab

Declarative OpenShift platform, managed end-to-end by Argo CD (GitOps).

## Principle
Everything that can be declarative IS declarative. The only imperative step is
the one-time bootstrap of Argo CD itself (chicken-and-egg). After that, every
change is a Git commit that Argo CD reconciles.

## Layout
| Path | Purpose |
|------|---------|
| `bootstrap/`        | One-time manual apply: Argo CD install + root app-of-apps |
| `clusters/local/apps/` | One Argo `Application` per component (sync-wave ordered) |
| `infrastructure/`   | Platform operators (OLM Subscriptions) — Kustomize base+overlays |
| `apps/`             | Workloads (e.g. openspeedtest) — Kustomize base+overlays |
| `charts/`           | Own Helm charts |

## Flow
bootstrap/root-app.yaml  ->  clusters/local/apps/*  ->  infrastructure/* & apps/*
