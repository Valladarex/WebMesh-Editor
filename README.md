# WebMesh Editor v2.0.00

WebMesh Editor is a single-file, browser-based Nastran deck viewer/editor for `.dat` and `.bdf` models.

## Major Upgrades Since v1.0.00

### 1) UI/UX Re-architecture
- Replaced the long-scroll sidebar workflow with static left-lane menus and viewport flyout panels.
- Added full Inspect/Create/Modify flyout flows with lock/unlock behavior.
- Added layout controls to hide/show left sidebar, right sidebar, and status dock.
- Reduced nested scroll behavior and improved panel density/readability.
- Added dedicated `Material` lane in create/modify workflows.

### 2) File Ingest + INCLUDE Resolution
- Added multi-file and folder loading paths for model + dependency ingestion.
- Added entry-deck chooser when multiple candidate `.dat/.bdf` files are found.
- Added INCLUDE-aware loading with virtual file system (VFS) handling.
- Added support for nested INCLUDEs and multiline INCLUDE path parsing.
- Added path-resolution fallback behavior for root/subfolder deck layouts.
- Added include-depth protection and clearer status feedback for include failures.

### 3) Schema Card Engine (Create + Modify)
- Replaced hardcoded create/modify forms with schema-driven field rendering.
- Added field-tier behavior (`Required`, `Recommended`, `Advanced`) and advanced-toggle control.
- Added card-category filtering so each menu shows relevant cards only.
- Modify path now applies targeted field updates (surgical edit behavior) instead of blanket delete/recreate.

### 4) Expanded End-to-End Card Support
- Parse/hydrate/edit/write coverage expanded across core card families, including:
  - `GRID`, `CORD1R/C`, `CORD2R/C/S`
  - `CTRIA3`, `CQUAD4`, `CTETRA`, `CHEXA`, `CPENTA`, `CPYRAM`
  - `CROD`, `CBAR`, `CBEAM`, `CBUSH`, `RBE2`, `RBE3`
  - `PSHELL`, `PSOLID`, `PROD`, `PBAR`, `PBEAM`, `PBUSH`, `PCOMP`, `MAT1`
  - `FORCE`, `MOMENT`, `LOAD`, `PLOAD2`, `PLOAD4`, `SPC`, `SPC1`, `CONM2`

### 5) Selection Tool Overhaul
- Unified selection manager across entities: nodes/elements/loads/constraints/properties.
- Added selection methods for element workflows: by normal, by face, by element type.
- Added operation modes: replace, add, remove, intersect.
- Added range/list apply modes with selection copy/paste support.
- Added selection transforms:
  - nodes-from-elements
  - elements-from-nodes
  - select-elements-by-property
- Improved selection-state stability (including Alt+drag teardown paths).

### 6) Model Tree + Context Menu Upgrades
- Model tree now supports richer type-group interaction and capped ID expansion.
- Hovering IDs can preview entities in the viewport.
- Right-click menu supports more consistent edit and delete operations.
- Improved entity routing for context actions (elements, properties, loads, constraints).

### 7) Spreadsheet/CSV Data Exchange
- Added Excel-friendly **Schema CSV** import/export for selected card data.
- Added CSV workflows for selected node data updates.
- Added Nastran card-token CSV import/export paths for controlled bulk edits.
- CSV flows preserve card identity (`card + id`) and support upsert behavior.

### 8) Large-Input Card Editors
- Added PCOMP layup table editing (row-based ply workflows).
- Added RBE large-node-list editing with append/replace/remove operations.
- Added bulk target-grid workflows for load/constraint card creation.

### 9) Transform and Utilities
- Split transform workflows into dedicated tools:
  - Linear Transform
  - Radial Transform
  - Reflect
  - Utilities
- Improved transform behavior for non-global coordinate-system cases.
- Expanded copy/reflect behavior across shells, solids, 1D elements, and rigid elements.

### 10) Visualization + Display Improvements
- Added/updated 1D center glyphs:
  - `CBUSH` spring glyph
  - `CROD` circle glyph
  - `CBAR` square glyph
  - `CBEAM` I-section glyph
- Improved property-driven element-face highlighting.
- Fixed UI/label layering so flyouts and labels render correctly.
- Made symbol/glyph size behavior viewport-relative for zoom stability.
- Updated default visual baseline tuning for symbol and spring size controls.

### 11) Export/Format Reliability
- Improved deterministic short/long/free format handling.
- Improved continuation handling and semantic-preserving export for supported cards.
- Reduced semantic drift in blank/default-sensitive fields (notably PCOMP workflows).

### 12) Sample and Distribution Behavior
- Updated the embedded sample model used by `Load sample`.
- Distribution remains single-file and offline-friendly.

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
