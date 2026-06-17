# Jarvis

**AI-powered personal knowledge wiki.** Ingest sources, synthesize knowledge, cross-link everything. Agent-driven curation on pure markdown.

## How It Works

```
Source (URL/File/Text) → source-raw/ → source-md/ → wiki/ → public/
                                    ↑           ↑
                                markitdown   synthesis
```

1. **Ingest** — Save the original to `source-raw/`, convert non-markdown via `markitdown` → `source-md/`, extract embedded media.
2. **Synthesize** — Read the converted markdown source, distill substantive knowledge into organized `wiki/` pages (one per topic), embed diagrams.
3. **Forge** — Promote topic to a polished public page in `public/` if it passes the verification threshold (no sensitive info, complete enough to share).
4. **Cleanup** — Update the catalog `map.md`, cross-link pages with wikilinks, check backlinks.

## Directory Layout

| Path | Purpose |
|------|---------|
| `source-raw/` | Original source files (pre-conversion) |
| `source-md/` | Markitdown-converted markdown files (date-prefixed slugs) |
| `wiki/` | Curated knowledge pages organized by domain hierarchy |
| `public/` | Publication-ready synthesis (polished, publicly shareable) |
| `temp/` | Working files / failed conversions |
| `map.md` | Catalog matching files to summaries and sources |
| `agents.md` | Master agent operations manual (behavior instructions for all agents) |
| `design.md` | UX/UI design specifications (Design Tokens, Typography, Palette, and User Flow Guidelines) |
| `architecture.md` | Software and pipeline architecture specification (directory layout and module communication) |
| `setup.md` | Developer environment setup and bootstrap verification guide |
| `tasks.md` | Shared agent task checklist for active runs (replaces agent-specific files) |
| `plan.md` | Shared workspace implementation proposal scratchpad (replaces agent-specific files) |
| `memory.md` | Project memory & context scratchpad (preferences, guidelines, run history) |
| `changelog.md` | AI agent activity changelog (append-only ledger tracking all agent runs) |

## Current Content

0 wiki pages. Ingest your first source to begin.

## Prerequisites

- `markitdown` — `pip install markitdown==0.1.1`
- AI agent with file + shell access (Zed, Claude Code, OpenCode, Antigravity)
- `git` — optional, recommended for recovery

## Operations

All agent behavior is defined in [`agents.md`](agents.md). Queries search `wiki/` and `public/` only — `source-md/` holds raw conversions, not curated knowledge.
