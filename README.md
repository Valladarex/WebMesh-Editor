# WebMesh Editor v2.2

WebMesh Editor is a single-file, browser-based Nastran deck viewer/editor for `.dat` and `.bdf` models.

## New in v2.2 - Changes Since v2.1

### 1) Large-Model Performance Recovery and Architecture Cleanup
- Reworked the large-model path around the forced SoA/core payload direction so small and large models stay on the same architecture.
- Added M8 baseline capture, forensic reporting, and deterministic regression coverage for render, coordinate, and clipping failures.
- Restored full filled-surface rendering for large decks instead of partial/wireframe-only behavior.
- Reduced large-model interaction cost by moving more truth to worker/core payload data and tightening main-thread selection/render paths.
- Added targeted regressions for:
  - coordinate truth (`tests/test_m8_p1_coord_contract.mjs`)
  - large render parity (`tests/test_m8_p2_render_parity.mjs`)
  - clipping/pick/select behavior (`tests/test_m8_p3_clip_selection.mjs`)

### 2) Clipping, Pick-Front, and Selection Fidelity
- Rebuilt clip-active element picking so visible front faces win instead of clipped-away/internal geometry.
- Restored box select, polygon select, `Show only`, and selected-subset rendering on the large model path.
- Fixed clipped selection so hidden entities behind the clipping plane no longer win point picks.
- Added front-visible node picking behavior so node picks stay aligned with what the user can actually see.
- Fixed clipping-plane UI and control issues:
  - actual default plane now matches the UI selector
  - numeric offset display is normalized to `.001`
  - numeric spinner arrows move in `0.1` increments

### 3) Viewport and Visual Fidelity Fixes
- Models now frame correctly on load/reset instead of opening off-screen or at unusable targets.
- 1D glyphs now respect depth occlusion instead of drawing through front geometry.
- Fixed glyph and clipping-plane viewport inconsistencies that made the scene look wrong even when geometry was correct.
- Added skybox support and related display controls.

### 4) Coordinate-System and Geometry Corrections
- Restored nested/local coordinate-system parity using explicit global node positions in the core payload.
- Fixed render-time coordinate resolution so local-coordinate nodes land in the correct global positions again.
- Corrected preserve-view geometry behavior after regressions in post-crash recovery work.

### 5) Post-Processing and Export Fixes
- Fixed MYSTRAN/F06 output handling beyond the original v2.1 release.
- Enabled support for STRESS, FORCE, GPFORCES, MPCFORCES, OLOAD, STRAIN
- Fixed `.dat` export behavior after the v2.1 release.
- Continued tightening deterministic export/roundtrip behavior while preserving the single-file offline workflow.

### 6) Reliability, Guardrails, and Auditability
- Hardened the read-gate proof system with signed metadata, freshness checks, similarity checks, and dedicated tests.
- Added post-crash audit, remediation, and performance forensic documentation so major regressions are tracked with evidence.
- Added watchdog and artifact-check tooling for long-running M8 performance work.

### 7) Release Scope Summary
- v2.2 is primarily a stability, performance, and interaction-fidelity release on top of v2.1.
- The biggest user-visible upgrades since v2.1 are:
  - large-model filled rendering restored
  - clipping and front-pick behavior fixed
  - coordinate-system regressions corrected
  - viewport framing and glyph occlusion fixed
  - skybox support added
  - export/post-processing fixes landed

## v2.1 Baseline - MYSTRAN Post-Processing (F06)

- Added **Analysis Results (MYSTRAN only)** workflow in Inspect mode.
- Added F06 parsing for:
  - nodal displacements (`T1/T2/T3`, total magnitude)
  - shell/solid/beam stress extraction with contour support
  - local element stress table components (Normal-X/Normal-Y/Shear-XY/Principal Major/Principal Minor/Shear-XZ/Shear-YZ/Von Mises where present)
- Added deformed-shape visualization with animation controls (`Play/Pause/Stop`, FPS, Speed).
- Added contour controls:
  - continuous/discrete coloring
  - color bin count
  - auto/manual min-max range
  - reverse palette option
- Added criteria overlays:
  - element criteria labels
  - node mode for displacement with direction arrows
  - configurable number formatting (scientific/real and sig figs)
- Added advanced legend controls:
  - viewport-anchored legend
  - manual text-size control
  - per-level tick labels matching contour formatting

## Controls

| Action | Control |
| :--- | :--- |
| Rotate | Left Mouse Button + Drag |
| Pan | Ctrl + Left Mouse Button + Drag |
| Zoom | Mouse Wheel |
| Pick Entity | Left Mouse Click |
| Box Select | Alt + Left Mouse Drag |
| Polygon Select | Ctrl + Shift + Left Mouse Click |
| Set Pivot | Double-Click on Model |
| Context Menu | Right Mouse Click on an entity |

## Usage

### Live Version
[LiveDemo(viaGitHubPages)](https://valladarex.github.io/WebMesh-Editor/WebMeshEditor.html)

### Local Version
Open `WebMeshEditor.html` (or `dist/WebMeshEditor.html`) directly in a modern browser.

No server process is required.