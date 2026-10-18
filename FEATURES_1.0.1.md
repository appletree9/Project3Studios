# Project3Studios V1 Sculpt — 1.0.1

This release adds an editable full human skeleton, real Blend/Merge geometry fusion, and draggable object transform handles. The frozen 1.0.0 folder and ZIP were left intact. Nothing was published or changed on GitHub.

## Run / GitHub Pages

Extract `Project3Studios_V1_Sculpt_1.0.1_APP.zip`. Upload **the contents of app/** to the root of your GitHub Pages source branch (usually `main`). Keep `index.html`, `anatomy-assets.js`, `sw.js`, `manifest.webmanifest`, and all icons together. Commit the changes, then use Settings → Pages → Deploy from a branch → your branch → `/ (root)`. No build step is needed. Your address remains https://appletree9.github.io/Project3Studios/.

Open the hosted page and refresh once. The new header says **FULL HUMAN ARMATURE · VERSION 1.0.1**. The service worker uses a new cache name. Three.js and the GLB exporter still require internet on first use. Use an HTTP server for local testing rather than opening index.html directly.

## Full skeleton

1. Add/select a detailed Male Body or Female Body, then open **Armature**.
2. Choose **Add / Replace Human Skeleton** (Create Rig is an alias). This binds an 82-joint hierarchy to the selected sculpt. It includes pelvis/root, spine/chest, neck/head, bilateral clavicles, shoulders, upper/lower arms, hands, all five fingers, upper/lower legs, feet and all five toes with tips.
3. **Rest placement**: select a joint from the hierarchy or tap a blue viewport handle. Gold is selected. Drag to move it; children follow. Local X/Y/Z number inputs allow precise placement. The drag constraint restricts movement to X, Y, Z, or the screen plane. Fit the generic preset to your particular model, especially fingers.
4. **Move whole skeleton** moves all root joints together while keeping the sculpt in its rest placement. The normal object transform controls reposition the entire character.
5. **Pose**: drag a joint to rotate it, or use the three rotation sliders. Pose rotations are stored separately and survive switching back to rest placement. **Reset Pose** clears rotations. Rest edits rebind and recalculate automatic weights.
6. **Undo Rig / Redo Rig** undo joint changes; the main Undo/Redo also preserves rig data. Bone names, child bones, coordinates, rotations and weights are saved in `.p3sculpt` projects. **Export Skinned GLB** exports actual bones, skin indices, normalized weights and bind matrices.
7. Close Armature to return to sculpting the rest mesh; reopen it to restore the saved pose preview. Sculpting while that mesh's armature preview is active is blocked with guidance. One rig preview is active at a time; multiple objects can retain their own saved rigs. OBJ/ordinary mesh exports continue to use the rest sculpt; use the armature GLB button for the rig.

Automatic weights use distance to bone segments. They are functional starting weights, not production hand-painted weights or anatomical constraints. This release adds no IK, animation timeline, joint limits, or new weight-painting system. External rigging software may be needed for fine shoulder/finger deformation. Physical iPhone performance and compatibility with every external GLB consumer remain unverified.

## Blend / Merge

In the Inspector, scroll to **BLEND / MERGE OBJECTS**. Check at least two objects (up to 12), position them so they overlap or touch across enough area, choose **Detail** and **Blend smoothness**, then choose **Blend checked objects**.

This voxelizes each solid separately, unions their occupied volumes, checks six-neighbor volume connectivity, creates one shared-vertex boundary, smooths the actual geometry, and recalculates normals. It is not grouping or overlapping hidden meshes. World positions, rotations and scales are baked into the result. The result is a regular sculptable indexed mesh.

Separated or unresolved thin contacts are rejected with instructions to overlap the objects or increase Detail. No automatic bridge is added. Open surfaces and very thin features may not voxelize reliably. Higher Detail retains more shape; more smoothing rounds transitions and can shrink fine features. The first checked object in list order supplies the material. Paint and rigs are not transferred to the fused result; Undo restores the source objects and their data. Save/Open preserves the fused mesh and later sculpt edits.

Sources remain in place until geometry creation succeeds. Phone/tablet limits are stricter, Detail is capped, and estimated triangle/raycast work is checked before processing. This is a synchronous remesher after its progress message paints; complex accepted operations can briefly pause the page. Reduce Detail or simplify meshes if a workload limit is reported. Detailed full-body pairs may require simplification before fusion.

## Removed object controls

By user request, the Move / Rotate / Scale object toolbar, its Inspector buttons, and the object viewport gizmo are completely removed. The separate skeleton joint handles remain available in Armature. Existing numeric object position/size fields remain. Earlier handle verification describes the previous build.

## Verification and source

See `TEST_RESULTS.md` for exact checks and limits. `Project3Studios_V1_Sculpt_1.0.1_COMPLETE.zip` includes the deployable app, development source, browser test harness and continuation notes. `Project3Studios_V1_Sculpt_1.0.1/` is the saved source folder. The app has no build step; `app/index.html` is authoritative.
