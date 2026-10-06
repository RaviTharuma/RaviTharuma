# AGENTS

RaviTharuma (GitHub profile) (`RaviTharuma/RaviTharuma`) — Source of the GitHub profile README shown on github.com/RaviTharuma (intro, stack and tool badges, stats cards).

## Workspace (HARD)

- Run agent sessions in **Herdr on DEV-001** (the shared dev seat), not as ad-hoc long-running sessions on laptops.
- Worktrees only under `<repo>/.worktrees/<name>`; remove them when done.

## Env / secrets (HARD) — Varlock

- All env/secrets/config go through **Varlock** (https://varlock.dev). Commit `.env.schema` only; never commit `.env*`, never `git add -f` them.
- No raw `.env`-only setups: every variable is declared in `.env.schema` (secrets marked `@sensitive`).
- Validate AI-safe with `varlock load --agent` (values redacted); scan before committing with `varlock scan --staged`.
- Agents read the schema, never secret values.

## Production / deploy infra (HARD)

- Customer production never runs on Tharuma/RaviTharuma personal Cloudflare, private domains, or Homelab (Tharuma infra: personal tooling and short-term staging/test only).
- Customer production runs on Novima/novmio or dedicated customer-brand infrastructure.
- This repo: Personal / fleet tooling. Running it on Tharuma infra (personal Cloudflare, Homelab) is fine for this repo itself; it must never become the host for any customer production workload.

## Issue tracking — Beads

- No Beads database here yet. For multi-session work, `bd init` against the fleet Dolt server instead of markdown TODO files; until then use GitHub issues.

## Repo conventions

- Keep the root docs (README, ARCHITECTURE, STACK, GLOSSARY, SECURITY) in sync with the code in the same PR.
- Add an entry to `CHANGELOG.md` under `[Unreleased]` for every meaningful change.
- Conventional commit subjects (`feat:`, `fix:`, `docs:`, `chore:`).
