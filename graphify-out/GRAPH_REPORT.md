# Graph Report - .  (2026-06-19)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 24 nodes · 43 edges · 4 communities
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `7911f762`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- [[_COMMUNITY_Community 0|Community 0]]
- [[_COMMUNITY_Community 1|Community 1]]
- [[_COMMUNITY_Community 2|Community 2]]
- [[_COMMUNITY_Community 3|Community 3]]

## God Nodes (most connected - your core abstractions)
1. `agents.md File` - 14 edges
2. `Bootstrap Script` - 14 edges
3. `wiki Directory` - 6 edges
4. `public Directory` - 5 edges
5. `map.md File` - 5 edges
6. `source-md Directory` - 4 edges
7. `Ingestion Pipeline` - 4 edges
8. `source-raw Directory` - 3 edges
9. `memory.md File` - 3 edges
10. `changelog.md File` - 3 edges

## Surprising Connections (you probably didn't know these)
- `Bootstrap Script` --creates--> `source-raw Directory`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 1 → community 0_
- `Bootstrap Script` --creates--> `wiki Directory`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 2 → community 0_
- `Synthesis Engine` --writes_to--> `wiki Directory`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 2 → community 1_
- `changelog.md File` --references--> `agents.md File`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 0 → community 3_

## Import Cycles
- None detected.

## Communities (4 total, 0 thin omitted)

### Community 0 - "Community 0"
Cohesion: 0.46
Nodes (8): Bootstrap Script, agents.md File, architecture.md File, design.md File, plan.md File, setup.md File, tasks.md File, temp Directory

### Community 1 - "Community 1"
Cohesion: 0.33
Nodes (7): Ingestion Pipeline, map.md File, source-md Directory, source-raw Directory, markitdown Tool, Registry Mapping, Synthesis Engine

### Community 2 - "Community 2"
Cohesion: 0.40
Nodes (6): Distillation Process, Forge Engine, public Directory, wiki Directory, Public Promotion, Query Flow

### Community 3 - "Community 3"
Cohesion: 0.67
Nodes (3): changelog.md File, memory.md File, System Tracking

## Knowledge Gaps
- **4 isolated node(s):** `markitdown Tool`, `Registry Mapping`, `Distillation Process`, `Public Promotion`
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `agents.md File` connect `Community 0` to `Community 1`, `Community 2`, `Community 3`?**
  _High betweenness centrality (0.374) - this node is a cross-community bridge._
- **Why does `Bootstrap Script` connect `Community 0` to `Community 1`, `Community 2`, `Community 3`?**
  _High betweenness centrality (0.374) - this node is a cross-community bridge._
- **Why does `wiki Directory` connect `Community 2` to `Community 0`, `Community 1`?**
  _High betweenness centrality (0.187) - this node is a cross-community bridge._
- **What connects `markitdown Tool`, `Registry Mapping`, `Distillation Process` to the rest of the system?**
  _4 weakly-connected nodes found - possible documentation gaps or missing edges._