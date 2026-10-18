# Project3Studios V1 Sculpt 1.0.1 — Header Slider r8

This release repairs armature posing and adds simpler rig choices and real rotation-keyframe animation. The detailed anatomy meshes, sculpting, painting, object transforms, Blend/Merge and PWA assets remain. The frozen 1.0.0 baseline was not edited. This chat has not published changes to GitHub.

## GitHub Pages

Extract `Project3Studios_HEADER_SLIDER_R8.zip`. Its website files are at the ZIP root: upload those files directly to your repository root, replacing the existing `index.html`, `sw.js` and other app files. There is no enclosing `app/` folder in this upload ZIP. Do not upload the ZIP itself as the website.

Keep anatomy-assets.js, manifest.webmanifest and the icons alongside index.html. Pages should deploy your source branch's `/ (root)` directory. No build step is needed. After deployment, the header must include **HEADER SLIDER r8**. Save your project before accepting an in-app update/reload notification. Three.js and GLB import/export modules require internet on first use. The service-worker cache ends in `r8`.

## Header slider

Use the slider below the header to reveal every option. The arrow buttons move through the header a page at a time. You can also swipe the options row on touchscreens, scroll with a mouse wheel/trackpad, or focus the slider and use the arrow/Home/End keys. Slider position follows direct scrolling and updates when the window resizes. Undo, Redo, Focus and Export remain available on small screens instead of being hidden. Existing header actions and its draggable grip remain functional. The bottom object toolbar remains removed.

## Start a rig

Select your sculpt and open **Armature**. Open **Rig presets · Simple / Human / Custom**, choose a preset, and choose **Create selected rig**. Creating a replacement asks before replacing an existing rig and its animation. Main Undo can restore the previous rig.

| Preset | Joints | Use |
| --- | ---: | --- |
| Simple (original) | 3 | Root → Spine → Head; bend a simple sculpt |
| Full Human | 82 | Pelvis/root, spine/chest, neck/head, shoulders/clavicles, limbs, hands/fingers, feet/toes |
| Humanoid | 22 | A simpler body skeleton without individual fingers or toes |
| Custom chain | 2 initially | Start with root + child, then add your own branches |

New rigs open in **Pose**, with usable rotation controls. The preset is a starting fit: edit joint placement for your particular sculpt, especially fingers. Old project rigs are retained. Saved non-finite, zero-sum or invalid weights are recalculated automatically on reopen.

## Edit joints

Choose **1 · Edit joints**. Search for a joint or select it from the visible hierarchy; the selected viewport joint is gold. Drag a joint in the screen plane or restrict movement to X/Y/Z. Children follow their parent. Local coordinate fields allow precise placement. Choose **Whole skeleton** to move all roots together. **Resize selected branch** changes descendant offsets by the entered percentage; it does not resize the sculpt.

Add a child joint or delete a branch. At least one root must remain. Animation keys are extended/remapped when joints are added/deleted. Rest edits rebind the mesh and recalculate weights; pose rotations and rotation keyframes are kept separately. Use **Undo rig / Redo rig** or the main Undo/Redo.

## Pose

Choose **2 · Pose**, select a joint, and use the X/Y/Z sliders or degree fields. Drag a colored ring for rotation around a local axis: red X, green Y, blue Z. Drag the gold joint for quick X/Z rotation, or choose a single joint-drag axis. The actual skinned mesh and child joints follow the rotation.

Reset one joint or the whole pose. **Mirror pose** copies a selected Left/Right branch to its counterpart in a human preset. **Parent** moves selection up the hierarchy; **Focus joint** recenters the view.

Opening Armature temporarily suspends sculpt/paint/object-drag interaction so joint gestures do not accidentally edit the sculpt or move the entire object. Closing restores the previous interaction mode and shows the rest sculpt. Reopen Armature to resume the saved rig/pose. On phones, background tool panels hide while Armature is open and return when it closes. The Armature panel remains draggable.

## Animate

1. Choose **3 · Animate** to open the timeline. At 0 seconds, set a pose and choose **Save pose key**.
2. Move the playhead to another time. Change the pose using the joint controls, then choose **Save pose key** again.
3. Choose **Play**, **Pause** or **Start**. Scrub the playhead or tap a saved key to inspect it. Toggle Loop as needed.
4. Edit an existing key by visiting its time, changing the pose and saving again. Delete a key with **Delete key**. Undo/Redo includes keys.

Keys store the whole skeleton's local rotations. Interpolation uses quaternion slerp. Edits are not auto-keyed: save a pose key after changing a pose. For a smooth loop, use matching poses at the beginning and end. Set clip name, length (0.1–60 seconds) and frames/second (1–60). Key times snap to the frame interval; a clip supports up to 300 pose keys. Deleting later keys is required before shortening a clip past them.

**Save Project / Open Project** keeps the hierarchy, rest placement, current pose, weights and all animation keys. **Export rig + animation GLB** exports a real skinned GLB, with animation tracks when there are at least two keys. The final key is held to the clip's duration if needed. The exported GLB was reimported and replayed in Three.js during testing.

This is rotation-keyframe animation. It does not add IK, joint limits, root-motion/position keys, or multiple clips per rig. Automatic weights are functional starting weights; production shoulder/finger deformation may need refinement in dedicated rigging software. Physical iPhone/pen hardware and every external GLB application remain untested. One rig preview is active at a time; each object can retain its own saved rig.

## Object movement and blending

The Inspector retains **Move / Rotate / Scale / Sculpt**. Object Move has labeled world-axis arrows and Scale has labeled local-axis cubes (red X, green Y, blue Z); rotation rings are available too. Object axis handles are hidden while Armature is open. Mouse/touch/pen capture, move constraints, grid snapping, undo/redo and saved transforms remain. The floating bottom Move / Scale / Sculpt bar stays removed.

For **Blend/Merge**, check two to twelve closed objects in the Inspector, position them in contact/overlap, choose Detail and Blend smoothness, then Blend checked objects. This performs an actual voxel union and smooths the shared-vertex geometry. It rejects disconnected solids rather than silently creating separate pieces. There is no automatic bridge; overlap the objects or increase Detail for unresolved thin contacts. Sources remain until creation succeeds; Undo restores them.

World transforms are baked into the result. The first checked object in scene-list order supplies its material. Paint and rigs are not transferred to the fused result; reapply them afterward. Save/Open preserves the fused sculpt. Detail is resolution-dependent; thin features can disappear and smoothing can shrink details. Phone limits are stricter, and high-complexity inputs can be blocked by workload estimates. Accepted remeshing can briefly pause the page.

## Saved source and verification

`Project3Studios_V1_Sculpt_1.0.1_COMPLETE.zip` contains app/, development sources, browser test harnesses, generated test projects/GLB and continuation notes. `app/index.html` is authoritative; there is no build pipeline. `development/armature-studio-r7.js` is a readable extraction of the final rig implementation, not a separately loaded app file. Historical patch scripts are intermediate work and must not all be rerun against the final app.

See TEST_RESULTS.md for final checks and limits. Ordinary OBJ/mesh exports use the rest sculpt; use the Armature GLB exporter for the skin and animation.
