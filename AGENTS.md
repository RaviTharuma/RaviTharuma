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

## Naming (HARD)

Name every new identifier with this grammar. Do not invent a second style.

Semantic skill: https://github.com/thonymg/skills/tree/main/skills/naming-convention
Go only, extra: https://github.com/cxuu/golang-skills/blob/main/skills/go-naming/SKILL.md

- A function is a verb: `fetchUser`, not `userData`.
- A boolean starts with `is`, `has`, or `can`.
- A file is named after the thing inside it. One type per file.
- One word for one concept. If the repo says `user`, do not also say `account` or `member` for the same thing.
- Forbidden: `data`, `info`, `temp`, `helper`, `manager`, `utils`, `misc`, `common`, `stuff`.
- Do not repeat the owner in the name: `user.name`, not `user.userName`.
- Abbreviate only words already used in this repo (`id`, `url`, `ssh`). Otherwise spell them out.
- A new term is written down once, then used. Do not invent a synonym in passing.
- An existing file in the same directory wins when that directory is already consistent.
- Casing follows the language:
  - Rust: `snake_case` functions, `PascalCase` types, `SCREAMING_SNAKE_CASE` consts. Clippy wins.
  - Go: `MixedCaps` / `mixedCaps`. Constants are `MaxSize`, never `MAX_SIZE`. Packages are lowercase, one word.
  - Swift: types `PascalCase`, methods and variables `camelCase`, file name matches the type.
  - TypeScript: `camelCase` variables and functions, `PascalCase` types and components, `kebab-case` module files.
  - Shell: `lower_snake_case` variables and functions, `UPPER_SNAKE_CASE` constants.
