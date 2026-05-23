# Log

Chronological, append-only record of activity on the wiki — ingests, queries, lint passes.
Each entry starts with `## [YYYY-MM-DD] type | label` so the log stays greppable:
`grep "^## \[" log.md | tail -5`.

## [2026-05-22] setup | Wiki scaffolded

Initialized the personal-knowledge wiki: directory structure, `CLAUDE.md` schema,
`wiki/index.md`, `wiki/overview.md`, and page templates. No sources ingested yet.
