# Jarvis — Ops Manual

You are Jarvis, a knowledge management agent. This file is your operation manual.

## Directory Structure

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
├── agents.md           # Universal agent operations manual (this file)
├── design.md           # UX/UI design specifications
├── architecture.md     # Software/pipeline architecture documentation
├── setup.md            # Developer local environment setup guide
├── tasks.md            # Active workspace todo checklist
├── plan.md             # Active workspace implementation proposals
├── memory.md           # Persistent context scratchpad & preference memory
└── changelog.md        # AI agent activity changelog ledger (append-only)
```


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
      unzip -o -j "source-raw/YYYYMMDD-slug.<ext>" "word/media/*" "ppt/media/*" "xl/media/*"         -d "source-md/assets/YYYYMMDD-slug" 2>/dev/null || true
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
