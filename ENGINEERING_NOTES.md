# Engineering Notes: Agentic RAG — Neo4j + Chroma + Gemini

Date: 2025-08-31

This document tracks upgrades, rationale, and next steps.

## Recent changes

- Routing
  - Fast semantic is gated to semantic intent only; complex queries go planner→KG.
  - Guard strips `@search_mode` prefix.
- Retrieval
  - Added lightweight query expansion using metric aliases.
  - Reused persistent Chroma vector store via `get_vectorstore()`.
  - Added simple rerank boosting metric/period mentions.
- KG
  - Cached Neo4j driver via `get_neo4j_driver()`.
  - Cypher returns `pred` for hygiene; series is filtered to dominant predicate and de-duplicated by period.
  - Coverage computed (have/requested) and used by judge.
  - Relax records `__relax_used__` in meta.
  - Heuristic table extraction fallback for series when KG returns nothing.
- Entity resolution
  - Fuzzy fallback with `difflib.get_close_matches` over fulltext top-10.
- UI
  - Added meta badges: Relax used, Coverage have/requested in Search mode.

## Known gaps / next steps

- Units & currency normalization with scaling (millions/billions) before math.
- Canonical metrics map (GAAP vs non-GAAP; segment-level) to avoid noisy predicates.
- Multi-entity comparison support (align series for multiple EIDs).
- Table-aware structured extractor (column labeling, unit parsing) instead of regex.
- Retrieval fusion (BM25 + dense) and table/document priors.
- Index-friendly Cypher: precomputed `predicate_lc` and equality/IN matching.
- Observability: timings, hit counts, route metrics; small eval harness with golden Qs.

## Quick test prompts

- "Trend of Verizon operating revenue over the last 6 quarters."
- "Plot the trend of capital expenditures for the last 6 quarters."
- "Compare Verizon operating revenue 2023-Q4 vs 2024-Q4."

## Rollback plan

- All changes are localized; to disable heuristics, remove `pred` filtering, table extraction, and meta badges.
