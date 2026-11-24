# FIX — all141layers and30,599deposition moves in3D

Source: `FIX_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode`. The legacyAll139Layers basename is retained. Final modelZ8.460mm.

Download raw HTML and open it locally to rotate, select layers, separate them visually or toggle travel/wipes. Hover shows E, speed, nominal width, fan and K. No source moves are simplified; display arcs are sampled at≤0.0002mm chord error. Centerlines do not represent measured bead width. Startup/purge and final parks are excluded.

Approved mirrored channels startY123.500: left clockwise/right counterclockwise, scarf E/Z retained. All deposition after layer10 usesK0.05. Lead-ins11–18 useflow0.98 baked into E, with original25mm/s printing speed and endpoints; no extra slow-start or priming. Lead-ins1–10 retainK0.55/flow1.4. Custom reverse wipes are removed; source slicer-loop wipes remain.

## Conditioning line after layer10

After the tenth scaffold layer and the existing245°C/K0.05 transition, a single40mm conditioning line prints from **X90,Y95 to X130,Y95 at build-plate Z0.060mm**. It uses nominal width0.212876mm, flow0.98 baked into E, speed3mm/s, K0.05 and part fan off, matching the first channel road. The line usesE0.19556949mm of1.75mm filament.

XY transfers to and from the remote line occur at **Z5mm** via the outside corridors. It finishes with a stationary0.4mm retraction and no reverse wipe. The original parked entry state atX20,Y220,Z5 is restored before the unchanged layer11 path. The closest model Y is114.710299, leaving **19.710299mm** clear of the line.

The existing startup mesh rectangle is expanded toX89..144.154984,Y94..143.439701 to cover this added build-plate road. No new probing/calibration sequence, thermal wait or layer marker is added. All prior model commands and scarf profiles remain unchanged; the full/test files still print141/18nominal layers. In the3D viewer, the conditioning line belongs to the completed-layer10 processing interval but its actual Z remains0.060mm.
