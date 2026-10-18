# Verification — Header Slider r8 / Armature Studio r7

18 October 2026. Final local app tested in headless Chrome with WebGL software rendering and a touch-enabled phone-sized context. All inline JavaScript and service-worker syntax checks passed. No application JavaScript errors were recorded in the final runs.

## Armature posing and presets

- Created Simple (3 joints), Full Human (82), Humanoid (22), and Custom Chain (2) through the actual UI. All opened in Pose with enabled controls.
- Checked all vertex influences for finite normalized weights, valid bone indices and successful skin deformation. Sample maximum displacements in the preset tests were approximately 0.756, 0.859, 0.859 and 0.301 model units, respectively.
- Actual mouse range input and degree fields changed bone rotations and deformed the skinned mesh. Pose Undo/Redo passed.
- Edit joints reset preview rotations to neutral while preserving the separate pose. Rest coordinate editing and return to the preserved pose passed.
- Custom child addition and branch deletion passed. A mouse drag on a local rotation ring changed the selected joint.
- Actual emulated touch slider dragging and touch viewport-joint posing passed.
- A saved rig containing a deliberately invalid/null weight was reopened; invalid weights were recalculated and all resulting weights were finite and normalized.

## Animation and export

- On a detailed Female Body, saved whole-pose keys at 0 and 1 seconds, with a 60° lower-arm rotation in the second key.
- At 0.5 seconds the sampled rotation was 30°, matching quaternion interpolation.
- Play advanced the clock and the joint pose; Pause stopped progression; Start returned to 0. Key Undo/Redo passed.
- Save Project through the actual button and reopening through the real project file input preserved the 82-joint rig and both keys. Closing/reopening Armature retained the animation.
- Export produced valid GLB bytes containing an 82-joint skin and 82 rotation channels. Reimported those exact bytes with GLTFLoader, played the imported clip with AnimationMixer, and verified the 30° midpoint rotation.

## Existing features retained

- Inspector Move/Rotate/Scale buttons were visible and clicked; each transformed an object correctly with mouse and touch, without changing mesh vertices or camera position. Undo/Redo passed.
- Viewport object Move/Rotate/Scale handles passed mouse/touch drags on an already transformed object. Move grid snapping, selected-object tracking, Undo/Redo and project save/reopen passed. Chrome-emulated pen dragging passed; physical pen hardware was not tested.
- Bottom `p3AxisDock` toolbar remained absent.
- Blend/Merge regression: two overlapping transformed solids became a connected 3,032-triangle indexed surface. All boundary edges were shared by exactly two triangles. Existing sculpting, Undo/Redo and snapshot restoration passed; disconnected input was rejected and source objects remained. Earlier actual merged-project Save/Open checks are retained in development/test-results.json.
- Detailed anatomy assets, icons, manifest and PWA structure were retained. Service worker uses a fresh r7 cache. Frozen 1.0.0 app hashes were checked against its saved inventory during packaging. ZIP entries were compared to their source files with SHA-256.

## Limits

These are representative tests, not exhaustive checks of every browser/model/tool. Physical iPhone speed/memory, physical pen behavior, every external GLB application, complex/open/nonmanifold merge inputs and production-quality shoulder/finger weighting remain unverified. The animation system keys local rotations; it has no IK, root-motion/position keys, joint limits or multiple clips per rig. Automatic weights are starting weights, and generic skeleton placement needs fitting.

Tests captured the exact generated Blob bytes instead of relying on the OS/browser Downloads flow, which was canceled in this environment. Test-only hooks were inserted by a local server and are absent from the shipped app. Full physical-device offline/PWA installation behavior was not rerun. The published site was not changed by this chat.


## Header slider r8

Tested the revised app in desktop (1440px, then resized to 900px) and phone (390px) Chrome contexts. Every main header action (Sculpt, Camera, Undo, Redo, Focus, Save, Open, Export OBJ, theme and Armature) was visible and could be scrolled fully into view. Native slider Home/End reached both ends with synchronized disabled arrow buttons. Arrow scrolling worked. The actual Armature button opened its panel and Close worked after reparenting. Phone native swipe and touch slider dragging worked. Desktop header dragging and window resizing retained the slider behavior. The bottom object bar was absent. No application JavaScript errors were recorded. Existing r7 armature/animation checks above were run before this header-only revision; its Armature action was rechecked in r8.

Header text cleanup: removed ARMATURE STUDIO · HEADER SLIDER r8 from the visible build label. All functionality retained. Cache suffix r8-clean. Static source check passed.
