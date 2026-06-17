# Project Memory & Context

This file serves as the long-term memory, state tracker, and collaboration log for all AI agents working in this repository.

## User Preferences & Guidelines
- Focus on maintaining high fidelity, curated knowledge in `wiki/`.
- Ensure all public-facing pages in `public/` strictly exclude sensitive or project-identifiable information.
- Prefer portable markdown links over filesystem symlinks for documentation cross-references.

## Current Goals & Tasks
- [ ] Ingest new raw sources and keep the wiki updated (user-driven).

## Agent Run History

| Date | Agent/Model | Action/Summary |
|------|-------------|----------------|
| YYYY-MM-DD | System | Initialized workspace layout and template operational files. |

## Key Decisions & Lessons Learned
- **Decisions**:
  - Unified the operations manual into `agents.md` to support Gemini, Claude, and OpenAI agents equally.
  - Retained `claude.md` as a redirect pointer to `agents.md` to avoid breaking any existing configurations or tools looking for it.
  - Implemented `memory.md` as a scratchpad for cross-agent collaboration and persistence.
  - Chose clear, self-descriptive directory names (`source-raw`, `source-md`, `wiki`, `public`) and placed index files (`map.md`) at the root for simpler navigation.
