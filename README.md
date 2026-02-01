# WebMesh Editor

A lightweight, in-browser editor for viewing, modifying, and creating simple Nastran (.dat, .bdf) finite element models. This tool is a single, self-contained HTML file with no server-side dependencies, making it easy to run offline or host on any static web server.

[LiveDemo(viaGitHubPages)](https://valladarex.github.io/WebMesh-Editor/WebMeshEditor.html)

## Key Features

#### Visualization & Display
* 3D Viewport: Interactively rotate, pan, and zoom complex finite element models.
* Display Customization: Toggle visibility for individual entity types, switch to property-based coloring, adjust symbol sizes, change background color, and enable smooth shading.
* Clipping Plane Tool: Slice the model along XY, YZ, or XZ planes to inspect internal geometry.
* Parallel View: Switch between a perspective and an orthographic (parallel) camera for easier alignment checks.
* Dynamic Camera Pivot: Double-click anywhere on the model to set the camera's rotation pivot point.
* Label Culling: Intelligently hides overlapping labels to prevent visual clutter on dense models.

#### Modeling & Editing
* Entity Creation: Add new Nodes (GRID), Elements (CQUAD4, CTRIA3, CBAR, etc.), Coordinate Systems (CORD2R), Loads (FORCE, MOMENT), and Constraints (SPC1).
* Interactive Editing: Click to select entities, use Alt+Drag for box selection, and use Ctrl+Shift+Drag for polygon selection.
* Advanced Coordinate Systems: Full support for parsing, visualizing, creating, and exporting nested CORD2R local coordinate systems.
* Undo/Redo: Full history support for all model modification actions.
* Copy Node Coordinates: Easily copy the coordinates from a selected node when creating a new one.

#### Transform Tools
* Linear Move & Copy: Translate or duplicate selections by a specific vector or by picking two nodes.
* Radial Move & Copy: Rotate or create circular patterns around a defined axis.
* Reflect: Mirror selections across a standard or user-defined plane.
* Mesh Refinement: Perform a 1-to-4 subdivision on selected shell elements to increase mesh density.
* Node Merging: Find and merge coincident nodes within a user-defined tolerance.

#### Inspection & Navigation
* Find by ID: Type a Node or Element ID in the selection panel and press Enter to find and highlight it.
* Model Tree: View a hierarchical summary of all entities in the model.
* Measurement Tools:
* 2 Nodes Selected: Shows the distance and ΔX, ΔY, ΔZ.
* 3 Nodes Selected: Shows the angle between them.
* Multiple Elements: Calculates the total area and centroid.
* Free Edge Display: Toggle a visual aid that highlights gaps or tears in a shell mesh.

## How to Use

#### Live Version (Recommended)
The easiest way to use the editor is via the GitHub Pages link above.

#### Local Version
Download the latest .html file from the repository and open it in a modern web browser.

## Controls
| Action | Control |
| :--- | :--- |
| Rotate | Left Mouse Button + Drag |
| Pan | Right Mouse Button + Drag |
| Zoom | Mouse Wheel |
| Pick Entity | Left Mouse Click |
| Box Select | Alt Key + Left Mouse Drag |
| Polygon Select | Ctrl + Shift + Left Mouse Drag |
| Set Pivot | Double-Click on Model |
| Context Menu | Right Mouse Click on an entity |

## Future Development Roadmap
The current version provides a solid foundation for viewing and simple editing. The long-term vision is to evolve this tool into a more powerful, lightweight pre-processor.

#### 1. Core Modeling & Meshing
* 3D Element Support: Add parsing, rendering, and creation support for CHEXA, CPENTA, CTETRA, and CPYRA solid elements.
* Advanced Meshing Tools:
* ~~Translate/Copy: Duplicate selections with a linear offset.~~(Completed in v0.98) 
* ~~Radial Copy: Duplicate selections around a center point and axis.~~(Completed in v0.98)
* ~~Reflect: Mirror selections across a defined plane.~~(Completed in v0.98)
* ~~Mesh Refinement: Subdivide existing shell elements to increase mesh density locally.~~(Completed in v0.98)
* ~~Node Merging: A utility to find and merge duplicate nodes within a given tolerance.~~(Completed in v0.98)

#### 2. Visualization & User Interaction
* Camera & View Controls:
* ~~Parallel Projection: Implement an OrthographicCamera mode for checking alignments.~~ (Completed in v0.80)
* ~~Dynamic Rotation Center: Snap the camera's pivot point to the entity under the cursor or a selected node.~~ (Completed in v0.80)
* Rendering Performance Optimizations:
* Instancing: Use InstancedMesh for rendering nodes and other repeated symbols to dramatically improve performance on large models.
* ~~Label Culling: Implement an algorithm to prevent labels from overlapping, ensuring readability.~~ (Completed in v-0.80)
* Progressive Loading: Use Web Workers to parse large files in the background without freezing the UI.

#### 3. User Interface & Experience (UI/UX)
* ~~Collapsible Panes: Allow sidebar sections to be collapsed to save space.~~ (Completed in v0.80)
* ~~Search & Filter: Add a search bar to find entities by ID.~~ (Completed in v0.98)
* Model Groups/Layers: Implement a system for users to create named groups of elements for easier visibility management.
* Hotkeys: Add keyboard shortcuts for common actions.

#### 4. Data & Compatibility
* Full Property/Material Support: Add UI panels and logic to create and edit PSHELL, PBAR, MAT1, etc.
* Long-Format Support: Implement import and export for 16-character field format cards.
* Export Selection: Allow exporting only the currently selected entities.

## Contributing
Bug reports, feature requests, and pull requests are welcome. If you find an issue or have an idea for an improvement, please open an issue in the repository's "Issues" tab.
