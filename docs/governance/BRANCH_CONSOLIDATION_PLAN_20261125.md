# Branch Consolidation Plan — jovfranco-tech (2026-11-25)

Cierre **local** del repositorio. No se hizo push, ni se tocaron ramas/tags remotos ni PRs.

- SHA de `main` antes: `9f31fd8`
- SHA de `main` después: el commit que introduce este documento (ver `git log -1 -- docs/governance/BRANCH_CONSOLIDATION_PLAN_20261125.md`); el SHA exacto se registra en `_consolidation_reports/cierre_d.md`.
- Bundle de respaldo (`--all`, verificado con `git bundle verify`): `C:\Repositorios\_aloria_backups\jovfranco-tech\jovfranco-tech-all-refs-20261125.bundle`
- Stash: ninguno.

## Clasificación de ramas

| Rama | Clasificación | Notas |
|---|---|---|
| docs/readme-reconciliation-001 (`ebd323d`, local + origin) | RETAIN | Solo README.md (+99/−1); PR #5 abierto. README público de perfil con métricas declaradas por el autor no verificables desde el repo; no se integró. Tag `archive/20261125/docs/readme-reconciliation-001`. |
| origin/docs/profile-positioning-20260725 (`bfb29ec`) | CLOSE | 0 commits por delante; PR #2 MERGED. Tag `archive/20261125/origin/docs/profile-positioning-20260725`. |
| origin/governance/ci-cost-optimization-v1 (`d3b139d`) | CLOSE | 0 commits por delante; PR #3 MERGED. Tag `archive/20261125/origin/governance/ci-cost-optimization-v1`. |

## Tags de archivo creados (locales, sin push)
- `archive/20261125/docs/readme-reconciliation-001`
- `archive/20261125/origin/docs/profile-positioning-20260725`
- `archive/20261125/origin/governance/ci-cost-optimization-v1`

## Ramas locales borradas

- Ninguna.
- `docs/readme-reconciliation-001` local se conserva: está checkout en un worktree externo (`C:/Users/jfran/.gemini/antigravity/scratch/aloria-readme-reconciliation-001/worktrees/jovfranco-tech`) y git no permite borrarla.

## PRs abiertos (no tocados)

- #5 — docs/readme-reconciliation-001 → main.

## Pendiente de autorización del dueño

- Decidir el PR #5 (revisar el README contra el código; integrar, ajustar o cerrar).
- Borrado de ramas remotas `origin/*` ya mergeadas/obsoletas y retirada del worktree externo.

