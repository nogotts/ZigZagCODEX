# FIX — approved mirrored18-layer diagnostic

`FIX_18layer_KammInletH_10PlatformPlus8ChannelLayers_SlowTravel.gcode` matches the full printing prefix through layer18/Z1.080, then parks and shuts down. No roof or upper inlets are printed. All eight channels start upward atY123.500, left clockwise/right counterclockwise, exact mirrors acrossX128. Existing scarf E/Z profiles are unchanged. Channel speed3then5mm/s remains unchanged.

All horizontal/diagonal lead-ins on layers11–18 use **K0.05 / flow0.98**, baked into E once; original25mm/s printing speed and endpoints are retained. No additional slow-start or extra priming is added. Layers1–10 retainK0.55/flow1.4.

Custom backward wipes are removed: stop, stationary retract0.4mm, lift, then travel. Original slicer-authored closed-loop wipes remain. No custom shake. Outside travel≤40mm/s, short raised approach/return20mm/s, Z10mm/s.

Full file: `FIX_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode`. The diagnostic has9,933deposition moves. LegacyPREVIEW text in a basename does not mean the mirror is pending; it is approved and applied.

## Conditioning line after layer10

After the tenth scaffold layer and the existing245°C/K0.05 transition, a single40mm conditioning line prints from **X90,Y95 to X130,Y95 at build-plate Z0.060mm**. It uses nominal width0.212876mm, flow0.98 baked into E, speed3mm/s, K0.05 and part fan off, matching the first channel road. The line usesE0.19556949mm of1.75mm filament.

XY transfers to and from the remote line occur at **Z5mm** via the outside corridors. It finishes with a stationary0.4mm retraction and no reverse wipe. The original parked entry state atX20,Y220,Z5 is restored before the unchanged layer11 path. The closest model Y is114.710299, leaving **19.710299mm** clear of the line.

The existing startup mesh rectangle is expanded toX89..144.154984,Y94..143.439701 to cover this added build-plate road. No new probing/calibration sequence, thermal wait or layer marker is added. All prior model commands and scarf profiles remain unchanged; the full/test files still print141/18nominal layers. In the3D viewer, the conditioning line belongs to the completed-layer10 processing interval but its actual Z remains0.060mm.

The40mm conditioning-line placement overview is now the first panel in the existing SVG/PNG. It showsX90,Y95→X130,Y95 at actualZ0.060, after layer10. The offline3D viewer highlights that line in green and provides a **40mm line(after10)** top-view button. Channel-loop distance/time labels still start from each channel’s own extrusion start and exclude conditioning/travel. This visual update does not change any G-code.
