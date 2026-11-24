# FIX — all141layers and30,598deposition moves in3D

Source: `FIX_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode`. The legacyAll139Layers basename is retained. Final modelZ8.460mm.

Download raw HTML and open it locally to rotate, select layers, separate them visually or toggle travel/wipes. Hover shows E, speed, nominal width, fan and K. No source moves are simplified; display arcs are sampled at≤0.0002mm chord error. Centerlines do not represent measured bead width. Startup/purge and final parks are excluded.

Approved mirrored channels startY123.500: left clockwise/right counterclockwise, scarf E/Z retained. All deposition after layer10 usesK0.05. Lead-ins11–18 useflow0.98 baked into E, with original25mm/s printing speed and endpoints; no extra slow-start or priming. Lead-ins1–10 retainK0.55/flow1.4. Custom reverse wipes are removed; source slicer-loop wipes remain.
