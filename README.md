# WebMesh Editor v2.2

WebMesh Editor is a single-file, browser-based Nastran deck viewer/editor for `.dat` and `.bdf` models.

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
