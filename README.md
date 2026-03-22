# WebMesh Editor v2.3

WebMesh Editor is a single-file, browser-based Nastran deck viewer/editor for `.dat` and `.bdf` models.

## New in v2.3 - Changes Since v2.2

### 1) Large-model runtime recovery
- Restored real large-model open after the post-`v2.2` regression period where some decks stalled around `99%` after parse.
- Removed the first-interaction freeze path that could hang the editor immediately after opening a large model.
- Large explicit box selection is now responsive again on real validated user decks because the editor no longer rebuilds a giant duplicate selected-face fill mesh for huge selections.
- Large-model interaction stays on the same runtime path as smaller models instead of relying on special-case deck-size behavior.

### 2) Copy / reflect / export / reimport stability
- Copy and reflect workflows were repaired so they work again on the restored large-model runtime.
- Reflected loads, moments, and coordinate systems now mirror with the correct direction/reference behavior instead of reversing or drifting.
- Export after copy/reflect no longer drops `CBAR` orientation or corrupts reflected metadata.
- Export + reimport now preserves the repaired reflect/copy results instead of reintroducing the earlier regressions.

### 3) Selection and viewport behavior
- Large box selection is much faster and stable enough for real large-model interrogation.
- Box select now latches from the initial `Alt` press, so releasing `Alt` during the drag does not collapse the gesture into a last-hover single pick.
- Releasing the mouse after rotate/pan/drag no longer accidentally selects the entity under the cursor.
- Shell hover highlighting uses a proper filled face tint without diagonal triangulation artifacts.
- `By face` shell picking was restored and behaves correctly again in the normal toolbar workflow.
- Element ID labels were restored when the label toggle is enabled.

### 4) Create / modify workflow recovery
- Direct modify-target selection was restored for properties, materials, loads, constraints, and coordinate systems.
- Grid and element modify workflows again use the existing `NID` / `EID` field instead of duplicate target-entry widgets.
- Create and modify reference fields now use inline combo inputs: you can type an ID directly or open a dropdown button inside the same field.
- Create defaults now seed from the next available live ID instead of reusing `1`, including new grids, loads, constraints, properties, materials, and coordinates.
- Create-element `Use Selection` now keeps connectivity inputs visible and fills them correctly instead of clearing the form.
- Property pickers are now type-aware:
  - shell elements only show shell-compatible properties
  - solid elements only show solid-compatible properties
  - `CBAR` only shows `PBAR`
  - `CBEAM` only shows `PBEAM`
  - `CBUSH` only shows `PBUSH`

### 5) Grouped load / constraint editing
- Load and constraint modify workflows now support grouped editing instead of forcing everything into one-record-at-a-time edits.
- Supported grouped workflows include:
  - `FORCE`
  - `MOMENT`
  - `PLOAD2`
  - `PLOAD4`
  - `SPC`
  - `SPC1`
- Mixed-definition records that share the same `SID` are no longer flattened together incorrectly; they stay as separate editable subgroups when their actual definitions differ.
- Grouped membership workflows now support add, append, replace, and remove actions from selection.
- `Remove Selected` is available for grouped node/element membership editing.
- Constraint component-only edits preserve the existing node set unless the user actually changes the membership list.

### 6) Schema, editor, and spreadsheet-style UX polish
- Long flyout panels now scroll instead of clipping off controls in the inspect tree or large modify forms.
- The `PCOMP` layup editor behaves more like a spreadsheet:
  - visible multi-cell selection
  - copy/paste workflows
  - single-value fill down a selected range
  - paste now replaces cell contents instead of appending text
- `PBUSH` now treats `K2..K6` as required instead of hiding them as advanced.
- `PSHELL` now requires `MID2`, `MID3`, and `MID4`, and seeds them from `MID1` by default to avoid unsafe solver behavior.

### 7) Display defaults and viewport polish
- Shading now defaults `ON`.
- Free-edge color now defaults to yellow.
- Free-edge line weight is thicker and easier to see.
- The status dock is stable on startup and user-resizable by dragging its edge.

### 8) Deletion and entity-management parity
- Modify mode now has explicit delete support for more entity types.
- Right-click delete parity was expanded so loads and constraints can be removed more like nodes and elements.
- Load/constraint delete behavior is now aligned with their dedicated selection modes.

### 9) MYSTRAN / F06 results upgrades
- One `.F06` file can now expose multiple result sets instead of collapsing everything into one overwritten flat result object.
- The results panel now lets you switch between:
  - subcases from a single run
  - modal eigenvector sets
  - buckling/eigenvalue result sets
- The results selector shows output-set metadata such as subcase, mode, eigenvalue, frequency/cycles, and load factor when available.
- `Output Vector` now only lists vectors that actually exist in the active result set instead of showing every possible result type all the time.
- Line elements now display contour colors instead of staying visually uncolored in result review.
- Full-wave contour playback now preserves opposite-direction contour colors correctly.
- Element criteria values now render again on element faces, including averaging nodal-result values onto the element face when `Criteria Mode = Element`.
- Results animation now supports both:
  - `Absolute`
  - `Full Wave`
- Results animation controls are more usable:
  - typed `FPS` entry
  - typed `Speed` entry
  - longer sliders for finer control
  - `FPS` range `1..120`
  - `Speed` range `0.01x..10x`
  - defaults of `30 FPS` and `1.00x`

### 10) Load-case / constraint / results visibility improvements
- In `.dat` model review, loads and constraints can now be filtered by subcase/load case from `Inspect > Visibility` instead of always showing every case at once.
- `SPC DOF` labels now render correctly on decks that use explicit scalar `SPC` cards, not just `SPC1`.
- Modify > Constraint for explicit `SPC` now shows the effective per-node DOF grouping instead of misleading single-row subsets when multiple scalar SPC rows stack on the same node.

### 11) Mass element fixes
- `CONM2` export no longer falls into the unwritable `ENDDATA` placeholder path.
- `CONM2` now has a dedicated ringed-disk glyph that is more visually distinct from a node at smaller sizes.

### 12) Release summary
- `v2.3` is primarily the recovery and workflow-hardening release after `v2.2`.
- The biggest end-user changes since `v2.2` are:
  - large models open and can be interrogated again
  - large selection is fast enough for real work
  - copy/reflect/export/reimport are materially more reliable
  - create/modify targeting is much easier and safer
  - grouped load/constraint editing is now viable
  - MYSTRAN/F06 results review is materially stronger, including multi-set output selection and better animation/contour controls
  - display, hover, picking, labels, and dock behavior are more consistent
  - `CONM2` mass support is safer in both export and visualization

## New in v2.2

### Large model improvements
- Large models now render as full shaded geometry again instead of falling back to widespread wireframe-only display.
- Large-model navigation and interaction are much smoother than in the late `v2.1` builds.
- Selection tools now behave much better on large models, including box select, polygon select, and `Show only`.

### Clipping and picking
- Clipping-plane selection now follows what is actually visible to the user.
- `Pick front` behavior is improved so visible faces and nodes win instead of hidden geometry behind them.
- Clipping controls are more reliable and easier to use, including manual offset entry.

### Display and viewport fixes
- Models frame correctly on load and reset instead of opening off-screen or at unusable positions.
- Glyphs now respect front geometry instead of drawing through the model.
- Labels, clipping, and viewport behavior are more consistent than in `v2.1`.
- Skybox support has been added.

### Coordinate and geometry fixes
- Nested and local coordinate-system rendering regressions from the `v2.1` upgrade work were corrected.
- Geometry placement is now more consistent between small and large models.

### Post-processing
- Enabled support for STRESS, FORCE, GPFORCES, MPCFORCES, OLOAD, STRAIN
- Improved F06/MYSTRAN post-processing support beyond the original `v2.1` release.
- Export behavior is more reliable than in the later `v2.1` builds.

### Summary
- `v2.2` is mainly a stability, usability, and large-model recovery release.
- The biggest end-user changes are:
  - better large-model rendering
  - better clipping and pick behavior
  - corrected coordinate-system behavior
  - better framing/reset behavior
  - improved post-processing support

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
