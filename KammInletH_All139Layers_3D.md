# Current Kamm assembly: all 141 layers and every model toolpath in 3D

The legacy `All139Layers` filenames are retained; their contents now represent **141 layers**, **30,576 model extrusion moves**, and a final printed height of **8.460 mm**.

Open the PNG for a static overview or the SVG for a scalable version. For the interactive viewer, choose **Download raw file** on the HTML’s GitHub page, then open the downloaded file in your browser. It includes its plotting library and works offline.

- Drag to rotate, scroll to zoom, and right-drag to pan.
- Select a single layer, a range, or all 141 layers.
- Add display separation to inspect buried lines; print geometry is not changed.
- Toggle travel, moving retractions/wipes, and stationary priming points.
- Hover to inspect the source G-code line, E, speed, nominal width and part fan.

Layers 1–10 are the retained platform. Layers 11–18 contain the new left/right eight-layer channels and all established lead-ins. Layer19 is the roof. The upper inlet continuation occupies layers 20–141. New channels print at 3 then 5 mm/s; the upper inlet continuation remains at 3 then 4 mm/s.

Every model extrusion move is represented at its actual XYZ coordinates, including scarf ramps. No extrusion moves are dropped or simplified. Arcs are sampled for display with a maximum chord error of 0.0002 mm. These are nozzle centerlines, not measured polymer widths. Startup/calibration/purge and final machine parking are excluded from model diagrams.

The viewer does not modify the G-code. Its validation JSON records the current G-code SHA-256, bounds, counts and layer statistics.

The current revision includes slower outside lead-in transfers, a 1 mm Z clearance, and the unchanged original wipe/retraction commands. No custom shake is added. Lead-ins use K0.55; channel paths retain K0.05. Toggle **Travel** to inspect the actual new routes.
