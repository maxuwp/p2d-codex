# Paper-to-Deck — Codex Plugin Changelog

Version format: `p2d_skill.X.Y`
- **X** (major): increment when accumulated changes warrant a new major release
- **Y** (minor): increment after each reflect session that produces universal improvements

Plugin version and skill version are kept in sync.

> Both the Claude Code plugin ([github.com/maxuwp/p2d](https://github.com/maxuwp/p2d)) and this Codex plugin share the same SKILL.md content and version number.

---

## p2d_skill.1.3 — 2026-06-21

**Initial standalone release.** Paper-to-Deck extracted from the POSED plugin into its own dedicated repository. All 13 skills at version 1.1 (content pipeline) or 1.2 (new skills), reflecting the three-stage architecture.

### Three-stage pipeline architecture

1. **Stage 1: Content Creation** — p2d-ingest (+ MCS/PSE extraction) → p2d-persona → p2d-outline (PSE-anchored, two-agent ≥85/100) → p2d-draft-slides + p2d-draft-notes → p2d-editor-review → Gate 1
2. **Stage 2: Humanization** — p2d-humanizer (32-pattern removal + presenter voice; zero em-dashes; /50, threshold 40) → Gate 2
3. **Stage 3: Visual Enhancement** — p2d-style → p2d-compile (3-preview template gate; humanized inputs; no image gen) → Gate 3

### Anti-divergence mechanism

`p2d-ingest` Pass C extracts MCS (Main Contribution Statement) + PSE (Primary Structural Elements) + paper_facts. Confirmed at HITL gate, locked in `manifest.canonical_facts`. Every downstream stage self-checks PSE coverage before opening its gate. Fixes AI drift (ASEE'26 demo: v00 covered only Phases 1–2 of a 4-phase paper).

### New skills

| Skill | Version | Purpose |
|---|---|---|
| `p2d-humanizer` | 1.1 | 32-pattern AI-tell removal + presenter voice; zero em-dashes; score /50 |
| `p2d-final-review` | 1.2 | Cross-artifact consistency audit (facts, citations, PSE coverage, MCS echo) |
| `p2d-reflect` | 1.2 | Extract preferences → `presentation_style.md`; log gaps; offer email draft |

### Plugin version

`.codex-plugin/plugin.json`: `1.3.0` (initial release of standalone p2d-codex plugin)

*Next reflection → p2d_skill.1.4*
