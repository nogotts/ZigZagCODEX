# FIX — approved mirrored18-layer diagnostic

`FIX_PREVIEW_Y123p5_MirroredChannels_LeftCW_18Layers.gcode` matches the full printing prefix through layer18/Z1.080, then parks and shuts down. No roof or upper inlets are printed. All eight channels start upward atY123.500, left clockwise/right counterclockwise, exact mirrors acrossX128. Existing scarf E/Z profiles are unchanged. Channel speed3then5mm/s remains unchanged.

All horizontal/diagonal lead-ins on layers11–18 use **K0.05 / flow0.98**, baked into E once; original25mm/s printing speed and endpoints are retained. No additional slow-start or extra priming is added. Layers1–10 retainK0.55/flow1.4.

Custom backward wipes are removed: stop, stationary retract0.4mm, lift, then travel. Original slicer-authored closed-loop wipes remain. No custom shake. Outside travel≤40mm/s, short raised approach/return20mm/s, Z10mm/s.

Full file: `FIX_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode`. The diagnostic has9,932deposition moves. LegacyPREVIEW text in a basename does not mean the mirror is pending; it is approved and applied.
