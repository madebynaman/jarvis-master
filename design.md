# Jarvis - UX/UI Design Specifications

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
