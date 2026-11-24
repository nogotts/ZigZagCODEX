# Bottom 100 µm channel: nozzle direction, starts and timing at 5 mm/s

The diagram is extracted from actual channel deposition moves in global layer12 (source channel layer2) of the current full G-code. No G-code was changed.

“Outer” means away from the center gap between the two objects. “Inner” means toward that gap. **Both channels print their physical left wall downward first, then their physical right wall upward.** That is outer-first on the left object and inner-first on the right object. Their traversal is not a reflection of one another.

The left loop first travels down toward its bottom inlet. The right loop travels up toward its top inlet and returns down the inner central wall before reaching the bottom inlet. Stars identify the actual first deposition points, including the start of each scarf ramp.

| Object | Bottom wall | Direction | Distance from own loop start | Time at 5 mm/s |
|---|---|---|---:|---:|
| Left | 1: outer | down | 5.407 mm | 1.081 s |
| Left | 2: inner | up | 18.025 mm | 3.605 s |
| Right | 1: inner | down | 36.175 mm | 7.235 s |
| Right | 2: outer | up | 48.719 mm | 9.744 s |

Distances count cumulative extruding XYZ motion from each loop's own first extrusion. Times are distance divided by 5 mm/s, not total wall-clock times. Travel, stationary priming and acceleration are excluded. The first channel layer actually prints at 3 mm/s; this figure represents the subsequent 5 mm/s layers.

The complete-loop overview uses actual XY coordinates and equal X/Y scale. Close-ups expand the horizontal scale for readability. Shaded nominal widths and computed nominal gaps are not measurements of the printed polymer. This diagram establishes a path-order difference; it does not prove that difference caused a blockage.
