# FIX — approved mirrored starts, directions and timing at5mm/s

Both channel loops start upward atY123.500. Left is clockwise and right counterclockwise, exact reflections aboutX128 on all eight channel layers. The sixteen-segment1.5mm scarf ramps are relocated with their original E/Z profiles. This diagram shows source channel layer2/global12.

| Passage point | Distance from each loop start | Time at5mm/s |
|---|---:|---:|
| First top wall |11.237mm|2.247s|
| First bottom wall (inner,downward)|40.806mm|8.161s|
| Second bottom wall (outer,upward)|53.349mm|10.670s|

Timing excludes travel, stationary priming and acceleration. Complete-loop overview uses actual XY; close-ups expand horizontal scale and shade nominal bead width, not measured plastic. Purple marks the relocated1.5mm scarf.

The full and18-layer files now use this approved mirror. Lead-ins11–18 and channels useK0.05; lead-in flow0.98. Custom reverse wipes are removed, with stationary endpoint retraction then lift. Source slicer-authored loop wipes remain. Lead-ins after layer10 keep25mm/s and their endpoints, with flow0.98 baked into E. No additional slow-start is added.

Source: `FIX_18layer_KammInletH_10PlatformPlus8ChannelLayers_SlowTravel.gcode`. The legacyPREVIEW basename, where present, is retained after theFIX prefix; approval has been applied.

The40mm conditioning-line placement overview is now the first panel in the existing SVG/PNG. It showsX90,Y95→X130,Y95 at actualZ0.060, after layer10. The offline3D viewer highlights that line in green and provides a **40mm line(after10)** top-view button. Channel-loop distance/time labels still start from each channel’s own extrusion start and exclude conditioning/travel. This visual update does not change any G-code.
