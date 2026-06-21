# Graph Report - .  (2026-06-19)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 27 nodes · 57 edges · 5 communities (3 shown, 2 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `f16daa77`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- [[_COMMUNITY_Community 0|Community 0]]
- [[_COMMUNITY_Community 1|Community 1]]
- [[_COMMUNITY_Community 2|Community 2]]
- [[_COMMUNITY_Community 3|Community 3]]
- [[_COMMUNITY_Community 4|Community 4]]

## God Nodes (most connected - your core abstractions)
1. `Jarvis` - 26 edges
2. `bootstrap.py` - 18 edges
3. `wiki` - 5 edges
4. `Ingestion Pipeline` - 5 edges
5. `Synthesis Engine` - 5 edges
6. `Forge Engine` - 5 edges
7. `source-md` - 4 edges
8. `Cleanup` - 4 edges
9. `source-raw` - 3 edges
10. `public` - 3 edges

## Surprising Connections (you probably didn't know these)
- `Jarvis` --references--> `agents.md`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 0 → community 3_
- `Jarvis` --references--> `Cleanup`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 0 → community 1_
- `Jarvis` --references--> `Graphify`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 0 → community 4_
- `Jarvis` --references--> `Ingestion Pipeline`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 0 → community 2_
- `Synthesis Engine` --references--> `wiki`  [EXTRACTED]
  jarvis.md → jarvis.md  _Bridges community 1 → community 2_

## Import Cycles
- None detected.

## Communities (5 total, 2 thin omitted)

### Community 0 - "Community 0"
Cohesion: 0.28
Nodes (13): architecture.md, bootstrap.py, changelog.md, design.md, .gitignore, Jarvis, memory.md, plan.md (+5 more)

### Community 1 - "Community 1"
Cohesion: 0.50
Nodes (5): Cleanup, Forge Engine, map.md, public, wiki

### Community 2 - "Community 2"
Cohesion: 0.50
Nodes (5): Ingestion Pipeline, Markitdown, source-md, source-raw, Synthesis Engine

## Knowledge Gaps
- **1 isolated node(s):** `Query`
  These have ≤1 connection - possible missing edges or undocumented components.
- **2 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Jarvis` connect `Community 0` to `Community 1`, `Community 2`, `Community 3`, `Community 4`?**
  _High betweenness centrality (0.669) - this node is a cross-community bridge._
- **Why does `bootstrap.py` connect `Community 0` to `Community 1`, `Community 2`, `Community 3`?**
  _High betweenness centrality (0.206) - this node is a cross-community bridge._
- **Why does `Ingestion Pipeline` connect `Community 2` to `Community 0`?**
  _High betweenness centrality (0.007) - this node is a cross-community bridge._
- **What connects `Query` to the rest of the system?**
  _1 weakly-connected nodes found - possible documentation gaps or missing edges._