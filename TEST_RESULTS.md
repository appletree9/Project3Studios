# Version 1.0.1 verification — 18 October 2026

Automated tests ran against the final local app in headless desktop Chrome with WebGL software rendering, plus a touch-enabled mobile browser context. No application JavaScript errors were recorded. All inline JavaScript passed Node syntax checks.

Passed:

- Male and female detailed body meshes: each 54,582 vertices and a full 82-joint skin. All four weight slots were checked for valid bone indices and weights summing to one.
- Lower-arm pose produced actual skinned vertex movement (maximum sampled displacement approximately 0.289 male / 0.216 female, in model units).
- Rest edits, rig Undo/Redo, hierarchy/pose restoration, and switching between neutral rest and retained pose rotations.
- Actual mouse pointer selection and dragging of a viewport head joint; actual emulated touch start/move/end selection and dragging.
- Existing GLB export button generated a valid GLB with an 82-joint skin. The binary JSON chunk was inspected. The OS/browser save-to-Downloads step was canceled by this environment, so subsequent export tests captured the exact generated Blob bytes through a test-only link interception. No such interception is shipped.
- Existing Save Project button serialized the edited skeleton/weights; reopening through the real file input restored the project. Test prompts were accepted automatically.
- Two transformed overlapping sphere solids fused into one regular indexed mesh at Detail 24 / smoothness 6 (3,032 triangles). Every undirected boundary edge occurred in exactly two triangles: no open edges or duplicated intersection seams. Voxel six-neighbor connectivity was checked by the implementation.
- The fused surface accepted the existing Inflate sculpt operation. Main Undo restored both sources; Redo restored the merged mesh. Snapshot restoration and actual project Save/Open preserved the merged geometry and sculpt edits.
- A spatially separated added solid was rejected and both input objects remained in the scene.
- Touch-context checkbox selection in the Blend list.
- Object Move/Rotate/Scale handles on an already rotated, scaled, off-center cube: actual mouse and emulated touch drags changed only the intended transform, with no mesh-vertex or camera changes. Undo/Redo and selected-object retention passed for all three modes.
- Object movement grid snapping, changed selection, actual project save/reopen of transforms, and toolbar dragging with mouse and touch passed. A Chrome emulated pen pointer drag passed; a physical pen was not tested.

Desktop and touch screenshots were visually inspected during development. Generic skeleton placement and fused surfaces were visible; screenshots also show the inherited draggable-panel layout, which users can rearrange/minimize.

Limits: these are representative tests, not exhaustive validation of every model, edit, legacy import/export/tool, browser, or device. Physical iPhone speed/memory, every external GLB consumer, production-quality finger weights, arbitrary open/nonmanifold inputs and complex accepted remesh workloads remain unverified. The mesh union is resolution-dependent; thin contacts can be rejected or fine details lost. Source meshes are preserved on reported fusion failure. No automatic connecting bridge is implemented; the UI requires sufficient contact/overlap.

PWA files and anatomy assets were retained. Service-worker JavaScript passed syntax checking; new cache naming was inspected. Full offline installation/update behavior was not rerun on a physical device. The published website was not changed.
