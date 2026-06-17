# Jarvis V0.2.6

Lean personal second brain. Pure markdown. No infra. AI-assisted ingestion, synthesis, and publishing.

This file is a self-sufficient guide to create a generalized, ready-to-use but empty clone of a Jarvis repository.

---

## 1. What Jarvis Is

Jarvis is a structured directory of markdown files that grows smarter with every source added. The directory itself serves as the source of truth. AI agents (like Zed + Claude Code, OpenCode, or Antigravity) read, write, and maintain the repository according to the operations manual. You curate raw sources and ask questions.

**Core loop:** Ingest → Synthesize → Cleanup

```
Source (URL/File/Text) → source-raw/ → source-md/ → wiki/ → public/
                                    ↑           ↑
                                markitdown   synthesis
```

---

## 2. Directory Layout

A complete Jarvis workspace contains the following directories and files:

```text
jarvis/
├── source-raw/         # Original source files (pre-conversion)
├── source-md/          # Markitdown-converted .md files (date-prefixed slugs)
│   └── assets/         # Media extracted during raw ingestion
├── wiki/               # Domain-organized curated knowledge wiki
│   └── assets/         # Images referenced by wiki pages
├── public/             # Publication-ready synthesis (polished, shareable)
├── temp/               # Working files / failed conversions
├── map.md              # Page catalog registry
├── agents.md           # Universal agent operations manual
├── design.md           # UX/UI design specifications
├── architecture.md     # Software/pipeline architecture documentation
├── setup.md            # Developer local environment setup guide
├── tasks.md            # Active workspace todo checklist
├── plan.md             # Active workspace implementation proposals
├── memory.md           # Persistent context scratchpad & preference memory
└── changelog.md        # AI agent activity changelog ledger (append-only)
```

---

## 3. Prerequisites

- **Python 3.8+**
- **pip** and **markitdown** (for converting non-markdown office documents and extracting media):
  ```bash
  pip install markitdown==0.1.1
  ```
- **Git** (optional, recommended for version history):
  ```bash
  git init
  ```
- An **AI agent with file + shell access** (e.g., Zed, Claude Code, OpenCode, Antigravity) running in the workspace directory.

---

## 4. Bootstrapping a New Workspace

To bootstrap a new, empty Jarvis workspace, save the following Python script as `bootstrap.py` in your target directory and run it. The script automatically creates the workspace folder structure and initializes all operational configuration files with their default clean templates.

### `bootstrap.py`

```python
#!/usr/bin/env python3
import os
import sys

# Define directories to create
directories = [
    "source-raw",
    "source-md",
    "wiki",
    "public",
    "temp"
]

print("Creating directories...")
for d in directories:
    os.makedirs(d, exist_ok=True)
    print(f"  Created: {d}/")

# Define file templates (completely generalized)
files = {}

# 1. readme.md
files["readme.md"] = """# Jarvis

**AI-powered personal knowledge wiki.** Ingest sources, synthesize knowledge, cross-link everything. Agent-driven curation on pure markdown.

## How It Works

___BACKTICKS___
Source (URL/File/Text) → source-raw/ → source-md/ → wiki/ → public/
                                    ↑           ↑
                                markitdown   synthesis
___BACKTICKS___

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
"""

# 2. agents.md
files["agents.md"] = """# Jarvis — Ops Manual

You are Jarvis, a knowledge management agent. This file is your operation manual.

## Directory Structure

___BACKTICKS___text
jarvis/
├── source-raw/         # Original source files (pre-conversion)
├── source-md/          # Markitdown-converted .md files (date-prefixed slugs)
│   └── assets/         # Media extracted during raw ingestion
├── wiki/               # Domain-organized curated knowledge wiki
│   └── assets/         # Images referenced by wiki pages
├── public/             # Publication-ready synthesis (polished, shareable)
├── temp/               # Working files / failed conversions
├── map.md              # Page catalog registry
├── agents.md           # Universal agent operations manual (this file)
├── design.md           # UX/UI design specifications
├── architecture.md     # Software/pipeline architecture documentation
├── setup.md            # Developer local environment setup guide
├── tasks.md            # Active workspace todo checklist
├── plan.md             # Active workspace implementation proposals
├── memory.md           # Persistent context scratchpad & preference memory
└── changelog.md        # AI agent activity changelog ledger (append-only)
___BACKTICKS___


## Distillation

Jarvis wiki is a shared second brain. Preserve all substantive knowledge from a source, reorganized
for clarity and cross-linked for navigation. Condensing means removing redundancy and
improving structure — never discarding substantive information.

All substantive knowledge from a `source-md/` source belongs in the `wiki/` directory. The only judgments are
how to organize it (pages vs sections) and which redundant/noise lines to drop.

KEEP (always): concepts and definitions; business rules and conditional logic; quantitative
thresholds, formulas, and calculations; worked examples; edge cases and exceptions; trade-offs
and rationale; workflow steps; diagrams and images; speaker notes that add meaning.

DROP (only these): redundancy (keep the single clearest framing, fold in unique nuance);
pure noise (logistics, filler, content-free presenter cues); conversion artifacts (page
numbers, broken fragments, empty refs).

Fidelity check: a source's wiki coverage should retain the substance of roughly its
informative portion, not a sliver. A 1,000-line source yielding 50 lines of wiki is a
defect — re-examine what was dropped.

Granularity: one wiki page per distinct topic. A rich source produces multiple pages.
Sub-topics too small to stand alone become sections within the parent page — never dropped.
Write each page to be understandable standalone by bringing needed context into the page.

**public page** — create only if:
1. Topic has enough depth to say something meaningful publicly.
2. Zero sensitive or identifiable information about any person, company, or project.
3. Content is polished, coherent, and complete enough to share as-is.
Fails → update wiki only. When in doubt — ask or skip.

## Page Format

Every wiki/ and public/ page follows compiled truth + sources + timeline:

    ---
    tags: []
    ---
    
    # slug
    
    > 2-3 sentence summary.
    
    [Current understanding — rewritable by agent.]
    
    **Sources:** [[YYYYMMDD-filename]], [[YYYYMMDD-filename]]
    
    **Generated-From:** [[YYYYMMDD-slug]]
    
    ## Timeline
    
    ### YYYY-MM-DD
    - Event description

- **Compiled truth:** Complete, reorganized capture of the source's substantive knowledge on
  this topic — rules, conditions, thresholds, formulas, worked examples, edge cases, trade-offs,
  and diagrams. Condense by removing redundancy and improving structure, never by dropping
  substance. Length is set by the topic, not a compression target. Rewritable when new evidence arrives.
- **Images:** Source diagrams are extracted to `source-md/assets/YYYYMMDD-slug/` at ingest. During
  synthesis, copy the images you embed into an `assets/SLUG/` directory alongside the page
  (e.g. page at `wiki/org/project/SLUG.md` → images at `wiki/org/project/assets/SLUG/`)
  and reference them with the full wiki-relative path. This keeps the wiki self-contained.
- **Sources:** Bare wikilinks to source-md files. Update when new sources are synthesized.
- **Generated-From:** wikilink to the source-md file(s) (provenance).
- **Tags:** Optional Obsidian tags; populate if useful, else leave `[]`.
- **Timeline:** Begins at the `## Timeline` heading. Append-only — never edit existing entries.
- **Contradictions:** Use `<!-- CONTRADICTION -->` marker + descriptive text.

## Wikilinks

Link to any page by filename slug: `[[slug]]`. Obsidian resolves by filename automatically.
- source-md files: `[[YYYYMMDD-slug]]`
- wiki/public files: `[[your-page-slug]]`

Every page must link to at least one other wiki/ or public/ page (skip only if none exists yet).
Slug rules are defined in Ingest below.

## Map (`map.md`)

One catalog, four tables:
- source-raw/: `File | Converted To`
- source-md/: `File | Notes`
- wiki/: `Slug | Summary | Sources`
- public/: `Slug | Summary | Sources`

Rules:
- One row per slug — replace in place on update; never append duplicates.
- Sort rows alphabetically by Slug (wiki/public) or File (source-raw/source-md).
- Summary reuses the page's 2-3 sentence summary, max 280 characters.
- Register source-raw/ + source-md/ rows during Ingest; wiki/ + public/ rows during Cleanup.

## Workflows

### Ingest

1. Receive source (URL, file, or text).
2. Build the slug: NFKD normalize → lowercase → alphanumeric + hyphens only → strip leading/trailing hyphens. Prefix today's date (from `date +%Y%m%d`): `YYYYMMDD-slug`.
3. Save the original to `source-raw/`:
   - URL → `curl -L "<url>" -o "source-raw/YYYYMMDD-slug.<ext>"` (ext from the URL; default `.html`). Fail → notify human, skip this source.
   - File → copy to `source-raw/YYYYMMDD-slug.<ext>` (keep the original extension).
   - Text → write to `source-raw/YYYYMMDD-slug.md`.
4. Produce `source-md/YYYYMMDD-slug.md`:
   - Raw is already markdown (text source, or a .md file) → copy it directly. No conversion.
   - Otherwise → `markitdown "source-raw/YYYYMMDD-slug.<ext>" -o "source-md/YYYYMMDD-slug.md"`. Fail → move the raw file to `temp/`, notify human, stop here (skip steps 5-6 for this source).
   - **Converter note:** The Read tool cannot parse binary DOCX/PPTX files — conversion is required. markitdown is preferred over web interface conversions (like Claude or ChatGPT uploads): it captures PPTX speaker notes (which contain substantive content web interfaces silently drop). For PDF files, the Read tool can parse natively; markitdown is optional but harmless.
   4b. Extract embedded media so diagrams survive. For Office files (.docx/.pptx/.xlsx):
      mkdir -p "source-md/assets/YYYYMMDD-slug"
      unzip -o -j "source-raw/YYYYMMDD-slug.<ext>" "word/media/*" "ppt/media/*" "xl/media/*" \\
        -d "source-md/assets/YYYYMMDD-slug" 2>/dev/null || true
    Remove the dir if no media was found. markitdown's own image refs are unreliable (names
    don't map to files) — treat the extracted assets/ files as the source of truth for visuals.
5. Register in `map.md`: source-raw/ table (File, Converted To) and source-md/ table (File, Notes).
6. → Synthesize.

### Synthesize

1. Read the source-md source fully. Capture ALL substantive knowledge — concepts, definitions,
   principles, patterns, decisions, business rules, conditional logic (if/then), quantitative
   thresholds and formulas, worked examples, edge cases, trade-offs, rationale, workflow steps,
   and diagrams. Drop only redundancy (keep the clearest single framing) and pure noise
   (logistics, filler, conversion artifacts). When in doubt, keep it — this is a wiki, not a
   highlight reel.
2. Cross-check wiki/:
   - No match → create a new wiki page (or add a section to a related page). Substantive
     knowledge always lands in wiki/; source-md/ holds only the raw conversion.
   - Match confirms → add the source to the Sources field only.
   - Match contradicts → add `<!-- CONTRADICTION -->` in compiled truth.
   - Match adds nuance → update compiled truth, add to Sources, add a Timeline entry.
2b. Organize by topic. A source covering multiple distinct topics produces one wiki page per
    topic; sub-topics too small to stand alone become sections within the parent page. Never
    collapse distinct topics into one page to save space. Embed meaningful diagrams from
    source-md/assets/YYYYMMDD-slug/ (architecture, workflows, scoring matrices, decision trees);
    skip purely decorative images. Copy the used images into a sibling `assets/SLUG/`
    directory (e.g. page at `wiki/org/project/SLUG.md` → `wiki/org/project/assets/SLUG/`)
    and reference with the full wiki-relative path (e.g. `wiki/org/project/assets/SLUG/imageN.png`).
3. Every page starts with a 2-3 sentence summary and follows the Page Format.
4. → Forge, then Cleanup.

### Forge (promote wiki → public)

1. For each wiki page created or updated this cycle, test it against the public threshold.
2. Threshold met → create or update the matching public page: a polished, public rewrite of the wiki page (same Page Format). Threshold fails → leave it in wiki only.
3. Before saving any public page, re-check: zero sensitive or identifiable information about any person, company, or project. When in doubt — ask or skip.

### Cleanup (post-synthesis)

1. Update `map.md` wiki/ (and public/, if promoted) tables.
2. Add wikilinks to connect related pages.
3. Backlink check: for each new/updated page, search wiki/ and public/ for its slug. Zero inbound links → add a cross-reference from a related page.
4. Log to `changelog.md`: Append a brief summary of the run.

### Query

1. Receive a question from the human.
2. Search wiki/ and public/ for relevant pages. (source-md/ holds raw conversions, not curated knowledge — do not search it.)
3. Nothing found → respond "The wiki does not have information on [topic] yet. Provide a source URL, file, or text for ingestion." Do not fabricate.
4. Answer from existing knowledge only. Cite sources with [[wikilinks]].

## Standards

### 1. Code & Document Styling
- **Markdown Consistency:** Use standard markdown with clean headers, bullet points, and code blocks.
- **Wikilinks:** Use `[[slug]]` format for linking wiki pages. Links must not contain backticks.
- **Embedded Media:** Image elements must use markdown format `![caption](wiki/path/to/assets/SLUG/image.png)`. Use absolute workspace paths or wiki-relative paths, ensuring the media resides in `assets/SLUG/` sibling to the page.

### 2. Naming Conventions
- **Slugs:** NFKD normalize → lowercase → alphanumeric + hyphens only → strip leading/trailing hyphens.
- **Source Files:** Prefixed with today's date (`YYYYMMDD-slug`).
- **Wiki & Public Pages:** Base slug name without date prefix (`your-topic-slug`).

### 3. Validation Criteria
- **Fidelity Check:** Distillation must capture the informative parts of sources, ensuring concepts, definitions, rules, workflows, and diagrams are not lost.
- **Backlink Integrity:** Every new/updated page must be cross-referenced from at least one other page in the wiki to avoid orphans.
- **Catalog Registry Sync:** Every file inside `source-raw/`, `source-md/`, `wiki/`, or `public/` must have a single corresponding entry in `map.md`.

## Planning and Execution

Every AI agent working on this repository MUST use the unified files `plan.md` and `tasks.md` in the root of the workspace to plan and track execution progress:
- **Planning (`plan.md`):** Before making complex changes, draft the proposed implementation plan in `plan.md` in the root. Present it to the user, request feedback, and wait for approval. Once approved, the plan can be executed.
- **Task Tracking (`tasks.md`):** Track all active execution steps inside `tasks.md` in the root using standard markdown checklists (`- [ ]`, `- [/]`, `- [x]`).
- **Post-Session Cleanup:** Upon completing a session or finishing a goal, update `plan.md` and `tasks.md` at the root to reflect the final state.

## Logs

- **Project Memory (`memory.md`):** Keep this scratchpad updated with recent goals, user preferences, key decisions, and agent run logs.
- **Activity Changelog (`changelog.md`):** Upon completing any session, append an entry tracking the date, time, app/harness, model name, and action summary in the exact format defined in `changelog.md`. Never modify or delete previous entries.

## Core Rules

- Use the system date for every date: `date +%Y%m%d` for slug prefixes, `date +%F` for Timeline headings.
- Update `map.md` on every change (see Map rules).
- Never edit timeline entries (append-only).
- Flag contradictions explicitly in compiled truth using `<!-- CONTRADICTION -->`.
- Never invent information. Only synthesize what exists in the wiki.
- Always quote file paths with double quotes in shell commands.
- Never put sensitive or identifiable information about any person, company, or project in `public/`. When in doubt — ask or skip.
"""

# 3. architecture.md
files["architecture.md"] = """# Jarvis - Software Architecture

This document describes the software architecture, repository organization, and technical workflow rules for the Jarvis wiki engine.

## Repository Overview

Jarvis is a markdown-based knowledge management system designed for multi-agent ingestion, synthesis, and publishing.

___BACKTICKS___
Source (URL/File/Text) → source-raw/ → source-md/ → wiki/ → public/
                                    ↑           ↑
                                markitdown   synthesis
___BACKTICKS___

## Core Modules & Data Pipeline

### 1. Ingestion Pipeline
- **Inputs:** Raw files (HTML, DOCX, PPTX, PDF, or text) or URLs.
- **Processing:** Converted to clean markdown via `markitdown` and saved into `source-md/` with date-prefixed filenames (`YYYYMMDD-slug.md`).
- **Media Extraction:** Any embedded assets (images, gifs) are extracted to `source-md/assets/YYYYMMDD-slug/`.

### 2. Synthesis Engine
- **Processing:** Converted markdown in `source-md/` is analyzed by an AI agent. The agent synthesizes and structures knowledge into `wiki/` pages based on domain hierarchy.
- **Granularity:** One file per distinct topic. Small subtopics remain as sections.
- **Cross-Linking:** Wikilinks (`[[slug]]`) are verified and updated to maintain a high-density, navigable web of documents.

### 3. Public Promotion (Forge)
- **Processing:** High-fidelity, polished, non-sensitive pages are promoted to `public/`.
- **Privacy Enforcement:** Strict checks ensure zero project-specific or personally identifiable information is leaked to public pages.

## Directory Layout Mapping

| Directory / File | Role in Architecture |
|---|---|
| `source-raw/` | **Storage Layer (Input):** Contains the original, unaltered raw source files (HTML, PDF, DOCX, PPTX, etc.) ingested from URLs or local paths. |
| `source-md/` | **Representation Layer:** Holds the standard Markdown conversions produced by the `markitdown` converter, using `YYYYMMDD-slug.md` names. Contains a nested `assets/` folder for extracted source media. |
| `wiki/` | **Distilled Knowledge Vault:** The core domain-organized knowledge pages. Each page represents a compiled topic summary. Sibling `assets/` directories hold referenced images. |
| `public/` | **Publication Layer (Output):** The polished, non-sensitive versions of wiki pages promoted for external sharing. |
| `temp/` | **Error / Staging Vault:** Staging files or inputs that failed conversion for developer inspection. |
| `map.md` | **System Registry:** Central index tracking the ingestion status, file names, summaries, and source lineages. |
| `agents.md` | **Agent Orchestrator Configuration:** The master operations manual directing all AI agent actions. |
| `design.md` | **Design System Specifications:** The guidelines for visual and layout formatting. |
| `setup.md` | **Bootstrap/Environment Config:** Instructions and scripts to configure dependencies and local folders. |
| `tasks.md` | **Workspace Task Ledger:** The shared checklist for agents to track current progress. |
| `plan.md` | **Workspace Implementation Workspace:** Proposal scratchpad for drafting plans before user approval. |
| `memory.md` | **Persistent Workspace Context:** Stores preferences, guidelines, and historical decisions across runs. |
| `changelog.md` | **Audit Trail:** Append-only logs showing agent run history. |

## Module Communication & Data Flow

___BACKTICKS___mermaid
graph TD
    User([User Input]) -->|1. Feed URL/File| Ingest[Ingestion Pipeline]
    Ingest -->|2. Store original| Raw[(source-raw/)]
    Ingest -->|3. Convert via markitdown| Conv[(source-md/)]
    Conv -->|4. Read and synthesize| Synth[Synthesis Engine]
    Synth -->|5. Write distilled knowledge| Wiki[(wiki/)]
    Wiki -->|6. Check public threshold| Forge[Forge Engine]
    Forge -->|7. Promote if safe| Public[(public/)]
    Synth & Forge -->|8. Register entries| Registry[map.md]
    AllLayers -->|9. Audit & Track| Logs[memory.md & changelog.md]
___BACKTICKS___

1. **Ingestion Pipeline:** Reads external files and writes the original version to `source-raw/`, and the converted `.md` text to `source-md/`. Embedded media inside files are extracted to `source-md/assets/`.
2. **Registry Mapping:** The Ingestion pipeline immediately catalogs new files in `map.md`.
3. **Synthesis Engine:** The agent reads from `source-md/` and writes/updates compiled files in `wiki/`. Sibling images referenced are copied from `source-md/assets/` to `wiki/.../assets/`.
4. **Promotion Pipeline (Forge):** The agent compares new/updated `wiki/` pages against the safety threshold (no PII or project details) and mirrors them to `public/` if compliant.
5. **System Tracking:** All pipelines write run context changes to `memory.md` and append events to `changelog.md` upon completion.
"""

# 4. design.md
files["design.md"] = """# Jarvis - UX/UI Design Specifications

This document outlines the core user experience and visual design standards for the Jarvis wiki project, serving as the design system reference.

## Design Philosophy
- **Clarity over Complexity:** Prioritize clear typography, structured margins, and high scannability.
- **Content-First:** Every design element must support the reading and distillation of markdown knowledge.
- **Premium Simplicity:** Avoid unnecessary visual noise; use subtle shadows, harmonious HSL colors, and micro-interactions.

## Design Tokens

### Color Palette
- **Primary Accent:** HSL tailored, vibrant but easy on the eyes (e.g., Indigo-500 for focal points).
- **Backgrounds:** Rich dark mode surfaces (e.g., Slate-900) and clean light mode surfaces (e.g., Slate-50).
- **Text:** High contrast but readable (e.g., Slate-200 for dark mode, Slate-800 for light mode).

### Typography
- **Headings:** Modern, clean, geometric sans-serif (e.g., *Inter*, *Outfit*, or *Roboto*).
- **Body Text:** Highly readable sans-serif optimized for long-form reading (e.g., *Inter*).
- **Code/Monospace:** Standard geometric monospace (e.g., *Fira Code* or *JetBrains Mono*).

### Spacing & Grid
- **Scale:** 4px baseline grid (4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px).
- **Line Height:** 1.6x for body text to optimize reading comfort.

## User Interface Guidelines (IDEs & Markdown Preview)
- **Scannability:** Headers (`#`, `##`, `###`) must have distinct visual separation (e.g., border-bottom for `##`).
- **Diagrams & Visuals:** Flowcharts, diagrams, and matrices must use a consistent canvas size and clean borders. Transparent or dark-mode-optimized backgrounds are preferred for diagrams.
- **Alerts & Callouts:** Use standardized callout boxes (like GitHub alerts) for emphasizing notes, tips, warnings, and rules.

## User Flow Guidelines

### 1. Ingestion Flow (User to Raw Storage)
- **Initiation:** The user provides a URL, raw file, or text input to the agent.
- **Conversion Feedback:** The system converts files using `markitdown`. If successful, the user is notified of the new file path in `source-md/`. If it fails, the raw file is moved to `temp/` and the user is alerted.
- **Registry Update:** The file is registered in `map.md` instantly, giving the user visibility into the ingestion state.

### 2. Synthesis Flow (Distilling to Wiki)
- **Distillation View:** The agent reads the parsed file, identifies distinct topics, and creates or updates files in `wiki/`.
- **Fidelity Check:** Sub-topics are kept as sections in parent pages rather than discarded.
- **Public Promotion (Forge):** If a topic meets the public threshold (polished, no sensitive details), it is promoted to `public/`.
- **Backlink Check:** The agent scans the wiki to ensure there are no orphaned files by creating connections.

### 3. Query Flow (Accessing Knowledge)
- **Search Scope:** Queries search `wiki/` and `public/` files only.
- **Confidence Threshold:** If the search finds no matches, the agent responds clearly that information is not yet available, and prompts the user to provide a source. It never invents facts.
"""

# 5. setup.md
files["setup.md"] = """# Jarvis - Developer Setup

Follow these steps to set up your local development environment for running the Jarvis ingestion and synthesis pipeline.

## Prerequisites

1. **Python 3:** Ensure Python 3.8+ is installed:
   ___BACKTICKS___bash
   python3 --version
   ___BACKTICKS___

2. **Pip & MarkItDown:** Install the markdown converter library:
   ___BACKTICKS___bash
   pip install markitdown==0.1.1
   ___BACKTICKS___

3. **Git:** Initialize Git if not already configured:
   ___BACKTICKS___bash
   git init
   ___BACKTICKS___

## Folder Setup
Create the required workspace folder structure:
___BACKTICKS___bash
mkdir -p source-raw source-md wiki public temp
___BACKTICKS___

## Dependency Verification
Run the bootstrap check script to ensure all tools and files are in place:
___BACKTICKS___bash
python3 -c "import os,sys; d=['source-raw','source-md','wiki','public','temp']; f=['agents.md','map.md']; sys.exit(0 if all(os.path.isdir(x) for x in d) and all(os.path.isfile(x) for x in f) else 1)" && echo "Bootstrap: OK" || echo "Bootstrap FAILED — re-check files and folders"
___BACKTICKS___
"""

# 6. map.md
files["map.md"] = """# Map

## source-raw/

| File | Converted To |
|------|-------------|

## source-md/

| File | Notes |
|------|-------|

## wiki/

| Slug | Summary | Sources |
|------|---------|---------|

## public/

| Slug | Summary | Sources |
|------|---------|---------|
"""

# 7. memory.md
files["memory.md"] = """# Project Memory & Context

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
"""

# 8. changelog.md
files["changelog.md"] = """# AI Agent Activity Changelog

An append-only ledger tracking all actions taken by AI agents working on this workspace.

## Format
All runs must append (never edit/delete past entries) in this format:

___BACKTICKS___markdown
### YYYY-MM-DD HH:MM:SS (Timezone)
- **Agent / Harness:** [e.g. Antigravity IDE, Claude Code, Zed]
- **Model:** [e.g. Gemini 3.5 Flash, Claude 3.5 Sonnet]
- **Summary of Actions:** [bullet points of actions taken]
___BACKTICKS___

---

### YYYY-MM-DD HH:MM:SS (Timezone)
- **Agent / Harness:** Bootstrap Script
- **Model:** N/A
- **Summary of Actions:**
  - **Repository Initialization:** Bootstrapped the empty Jarvis knowledge base workspace folders and operational metadata files.
"""

# 9. plan.md
files["plan.md"] = """# Implementation Plan

This file is used by AI agents to draft and review implementation plans for user goals.

## Current Plan

No active plan. Ready for the next agent run.

## User Review Required

None.
"""

# 10. tasks.md
files["tasks.md"] = """# Tasks

- [ ] Ingest new raw sources and keep the wiki updated (user-driven)
"""

# 11. .gitignore
files[".gitignore"] = """.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
"""

# 12. claude.md
files["claude.md"] = """# Jarvis Operations Manual

The operations manual for Jarvis has been renamed and made model-agnostic to support multiple agents (Gemini, Claude, OpenAI, etc.).

Please see: **[agents.md](agents.md)**
"""

print("Writing files...")
for filename, content in files.items():
    if os.path.exists(filename):
        print(f"  Warning: {filename} already exists. Skipping.")
        continue
    content = content.replace("___BACKTICKS___", "```")
    with open(filename, "w", encoding="utf-8") as f:
        f.write(content)
    print(f"  Created file: {filename}")

print("\nBootstrap complete! Jarvis is ready to go.")
```

---

## 5. Usage

To get started:
1. Initialize Git if desired.
2. Put any new files or documentation you want to import into `source-raw/`.
3. Prompt your AI agent to run the ingest and synthesis pipeline according to the rules in `agents.md`.