# Bottom 100 µm channel: nozzle direction, starts and timing at 5 mm/s

The diagram is extracted from the separate PREVIEW G-code at global layer12 (source channel layer2). Canonical full/diagnostic files are unchanged.

“Outer” means away from the center gap between the two objects. “Inner” means toward that gap. **Both channels print their inner bottom wall downward first, then their outer bottom wall upward.** Left is clockwise; right is counterclockwise. The paths, directions, start points, scarf profiles and extrusion are exact mirrors about X128.

Both loops start at Y123.500, travel upward toward their top inlet, and then return down the inner central wall before reaching their bottom inlet. Stars identify the actual first deposition points, including the start of each scarf ramp.

| Object | Bottom wall | Direction | Distance from own loop start | Time at 5 mm/s |
|---|---|---|---:|---:|
| Left | 1: inner | down | 40.806 mm | 8.161 s |
| Left | 2: outer | up | 53.349 mm | 10.670 s |
| Right | 1: inner | down | 40.806 mm | 8.161 s |
| Right | 2: outer | up | 53.349 mm | 10.670 s |

Distances count cumulative extruding XYZ motion from each loop's own first extrusion. Times are distance divided by 5 mm/s, not total wall-clock times. Travel, stationary priming and acceleration are excluded. The first channel layer actually prints at 3 mm/s; this figure represents the subsequent 5 mm/s layers.

The complete-loop overview uses actual XY coordinates and equal X/Y scale. Close-ups expand the horizontal scale for readability. Shaded nominal widths and computed nominal gaps are not measurements of the printed polymer. This is a proposed mirrored traversal for review. It does not guarantee a physical printing outcome.

## Preview G-code and scarf preservation

`PREVIEW_Y123p5_MirroredChannels_LeftCW_18Layers.gcode` contains the original first ten scaffold layers and then the proposed eight-layer mirrored channel stage. It is a separate diagnostic with a normal shutdown at layer18/Z1.080 mm. Canonical main and existing diagnostic files have not been updated.

Every right source layer is re-seamed to Y123.500 along its existing outer straight rail. Its complete new command path is then reflected about X128 to create the left side. The right contour is retained to sub-micrometre coordinate-rounding tolerance; the former left source is replaced by the exact right reflection as requested.

The uploaded first channel layer has no scarf and remains flat at 3 mm/s. On each of the following seven layers, both 16-segment scarf phases are moved to the new 1.5 mm seam. All original ramp Z values and individual ramp-in/taper-out E values, including the final E0 step, are preserved. The former scarf location becomes normal extrusion rather than a second scarf. Its now-collinear normal segments are merged into one move. The two remaining straight-rail E portions are allocated so total extrusion per layer remains exactly equal to the original right source.

Both sides retain the right source's speeds (3 then 5 mm/s), widths, acceleration, part cooling, 245°C nozzle, 70°C assembly bed setting, and K0.05. Primes and wipe/retraction amounts are unchanged. The existing lead-in geometry and K0.55 settings are unchanged; raised approach/exit waypoints are adjusted to the relocated source starts and wipes. There is no custom shake.

Validation checks all eight clockwise/counterclockwise orientations, pointwise mirroring, scarf Z/E profiles and right-layer total E. All non-channel extrusion moves match the current diagnostic.
