# All 139 layers and every model toolpath in 3D

Open `KammInletH_All139Layers_3D.png` for the static overview, or the SVG for a scalable version.

For the interactive viewer, open `KammInletH_All139Layers_3D.html` on GitHub, choose **Download raw file**, then open the downloaded HTML in your browser. It contains its own plotting library and works offline.

- Drag to rotate, scroll to zoom, and right-drag to pan.
- Select any single layer, a layer range, or all 139 layers.
- Add display separation between layers to reveal buried lines. This does not change the print.
- Toggle travel, moving retractions/wipes, and stationary priming points.
- Hover over a path to inspect its source G-code line, E, speed, nominal width, and part-fan PWM.

All **30,180 model extrusion moves** are represented at actual XYZ coordinates, including scarf Z ramps. Arcs are sampled for display with a maximum chord error of 0.0002 mm. No extrusion moves are dropped or coalesced. Lines represent nozzle centerlines, not measured polymer widths. Startup/calibration/purge and final machine parking are excluded from the model diagrams.

This viewer reflects the revised layers 11–16 diagonal lead-ins: their outer endpoints now match layers 1–10, while inward endpoints remain fixed. Generating the viewer does not modify G-code. The validation JSON records the current G-code SHA-256, per-layer counts and bounds.
