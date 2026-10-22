# Square-wave extrusion audit and controlled comparison

The directly uploaded square-wave file exceeded the transfer tool's 32 MiB limit. This audit uses the saved 60-pair repository original, SHA-256 `0e8e90e4ef110fd4b27dfa3d37e86fa78498bb3eabc691d9f3baecb2d95d9bf4`. Its equivalence to the new upload is not established. The uploaded OrcaSlicer holder was read directly.

The custom generator retained many unnecessary collinear sampling vertices from FullControl. It emits 1,227,600 model deposition commands, median length 0.030769 mm, minimum 0.007692 mm. At the 15 mm/s programmed speed, minimum-length segments would require approximately 1,950 commands per second if full speed were maintained. The same segments require approximately 130 commands per second at the 1 mm/s first-layer speed. These are command-density calculations, not measured printer throughput or proof of buffer starvation.

The holder has a 0.2 mm nozzle, nominal 0.20 mm width and 0.10 mm layers, with wider adaptive sections. Its median model segment is 0.43436 mm. It uses 250 C initially, 245 C thereafter; 75 C bed initially, then 60 C; part cooling approximately 22-29% after the initial layers; 0.4 mm retraction with wiping. The custom uses 0.15 mm width, 0.06 mm layers, 245 C nozzle, 85 C bed, 0/50% selected fan, and retraction without wiping.

Both files use relative extrusion, 100% flow override, and the same extruder limits. Neither contains an executable M900/M572 pressure-advance setting. Custom positive model E values match the intended rounded-bead volume calculation, with no zero or negative E moves during deposition. No extra mid-edge retracts or dwell commands were identified. Layer-to-layer XY placement and 0.06 mm Z increments are consistent. A simple hypothetical float32 accumulation simulation did not produce lost positive-E moves or substantial total underextrusion; actual Bambu firmware arithmetic was not inspected.

## Controlled comparison file

`SquareWave_Spacing_Matrix_10Layers_Coalesced.gcode` merges only consecutive same-direction, axis-aligned deposition moves at identical feed rate. It contains 54,000 model deposition commands (95.6% fewer). Every square corner, path endpoint, per-path E total at 1e-8 mm precision, speed, temperature, fan command, retraction, layer height, dwell, startup and shutdown is preserved. The existing SVG key still applies. All other command lines compare byte-for-byte identical.

This isolates segmentation. It is not a physically verified fix. The original two-second fan-settling dwell before lifting is intentionally retained so the comparison changes only segmentation. That dwell is an independently undesirable endpoint-oozing risk, but it does not command repeated stops throughout a straight edge.

The numeric extrusion audit is insufficient to establish smooth physical extrusion or layer adhesion. A physical A/B comparison is required to determine whether command density contributes to the reported pulsing. If the exact uploaded file differs from the audited repository original, upload a compressed ZIP so it can be read within the transfer limit.
