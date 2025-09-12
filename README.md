# WebMesh Editor

A lightweight, in-browser editor for viewing, modifying, and creating simple Nastran (.dat, .bdf) finite element models. This tool is a single, self-contained HTML file with no server-side dependencies, making it easy to run offline or host on any static web server.

### 

LiveDemo(viaGitHubPages)
(https://www.google.com/search?q=https://valladarex.github.io/WebMesh-Editor/)

## Key Features

* **3D Visualization**: Interactively rotate, pan, and zoom complex finite element models in a 3D viewport.
* **File Support**: Load models by dragging and dropping .dat/.bdf files or using the file selector.
* **Model Creation**: Add new entities to your model, including:
* Nodes (GRID)
* Elements (CQUAD4, CTRIA3, CBAR, CBEAM, CBUSH, RBE2, RBE3)
* Coordinate Systems (CORD2R)
* Loads (FORCE, MOMENT) and Constraints (SPC1)
* **Interactive Editing**:
* Click to select nodes, elements, loads, and constraints.
* Use Alt+Drag for box selection.
* Edit node coordinates (local and global), element properties (PID, connectivity), and more through a detailed selection panel.
* **Advanced Coordinate Systems**: Full support for parsing, visualizing, creating, and exporting nested CORD2R local coordinate systems.
* **Display Customization**:
* Toggle visibility for individual element types, loads, constraints, and nodes.
* Switch color modes from default to property-based coloring.
* Adjust symbol sizes, background color, and shell opacity.
* Enable smooth shading for better depth perception.
* **Model Inspection**:
* View a hierarchical model tree with entity counts.
* Toggle labels for Node IDs, Element IDs, loads, and SPCs.
* Use the **Measure Tool** to see the distance and deltas between any two selected nodes.
* **Undo/Redo**: Full history support for all model modification actions.

### ✨ New Features in v0.80
* **Clipping Plane Tool:** Added a "Clipping" card to slice the model along XY, YZ, or XZ planes. Position can be set to a selected node, and the offset is adjustable with a slider or Ctrl+Mouse Wheel.
* **Label Culling:** Added a "Cull Labels" option (on by default) to intelligently hide overlapping labels and prevent visual clutter on dense models. The flickering issue has been resolved.
* **Collapsible Sidebar Panes:** All cards in the sidebar can now be collapsed and expanded to create a cleaner workspace.
* **Dynamic Camera Pivot:** Double-clicking anywhere on the model now sets the camera's rotation pivot point for more intuitive navigation.
* **Parallel View (Orthographic Camera):** The parallel projection camera mode is now fully functional.
* **Copy Node Coordinates:** Added a "Copy Selected Node Coords" button to the Add Node card for easier workflow.

## How to Use

#### Live Version (Recommended)
The easiest way to use the editor is via the GitHub Pages link above.

#### Local Version
Download the latest .html file from the repository and open it in a modern web browser.

## Controls
| Action | Control |
| ----- | ----- |
| **Rotate** | Left Mouse Button + Drag |
| **Pan** | Right Mouse Button + Drag |
| **Zoom** | Mouse Wheel |
| **Pick Entity** | Left Mouse Click |
| **Box Select** | Alt Key + Left Mouse Drag |
| **Context Menu** | Right Mouse Click on an entity |

## Future Development Roadmap
The current version provides a solid foundation for viewing and simple editing. The long-term vision is to evolve this tool into a more powerful, lightweight pre-processor. The following features are planned for future releases:

#### 1. Core Modeling & Meshing
* **3D Element Support:** Add parsing, rendering, and creation support for CHEXA, CPENTA, CTETRA, and CPYRA solid elements.
* **Advanced Meshing Tools:**
* **Translate/Copy:** Duplicate selections with a linear offset.
* **Radial Copy:** Duplicate selections around a center point and axis.
* **Reflect:** Mirror selections across a defined plane.
* **Mesh Refinement:** Subdivide existing shell elements to increase mesh density locally.
* **Node Merging:** A utility to find and merge duplicate nodes within a given tolerance.

#### 2. Visualization & User Interaction
* **Camera & View Controls:**
* ~~**Parallel Projection:** Implement an OrthographicCamera mode for checking alignments.~~ (Completed in v0.80)
* ~~**Dynamic Rotation Center:** Snap the camera's pivot point to the entity under the cursor or a selected node.~~ (Completed in v0.80)
* **Rendering Performance Optimizations:**
* **Instancing:** Use InstancedMesh for rendering nodes and other repeated symbols to dramatically improve performance on large models.
* ~~**Label Culling:** Implement an algorithm to prevent labels from overlapping, ensuring readability.~~ (Completed in v0.80)
* **Progressive Loading:** Use Web Workers to parse large files in the background without freezing the UI.

#### 3. User Interface & Experience (UI/UX)
* ~~**Collapsible Panes:** Allow sidebar sections to be collapsed to save space.~~ (Completed in v0.80)
* **Search & Filter:** Add a search bar to find entities by ID.
* **Model Groups/Layers:** Implement a system for users to create named groups of elements for easier visibility management.
* **Hotkeys:** Add keyboard shortcuts for common actions.

#### 4. Data & Compatibility
* **Full Property/Material Support:** Add UI panels and logic to create and edit PSHELL, PBAR, MAT1, etc.
* **Long-Format Support:** Implement import and export for 16-character field format cards.
* **Export Selection:** Allow exporting only the currently selected entities.

## Contributing
Bug reports, feature requests, and pull requests are welcome. If you find an issue or have an idea for an improvement, please open an issue in the repository's "Issues" tab.
