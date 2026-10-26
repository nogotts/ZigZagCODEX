# New triangular speed array: 50 mirrored pairs

Fifty sequentially printed objects, each containing two mirrored triangular paths with 10 mm straight intro/outro ends. Each row contains ten uniformly scaled sizes, nominal tip spacing 0.1 through 1.0 mm in 0.1 mm increments. The original matrix's 0.3 mm geometry is the 1× baseline. All objects have ten 0.06 mm layers, total height 0.60 mm. Each pair is completed before moving left to right to the next pair, then to the next row farther back on the plate.

| Row (front to back) | IDs | First-layer speed | Layers 2–10 speed | Commanded width | Flow ratio |
|---|---|---|---|---|---|
| 1 | 01–10 | 5 mm/s | 2.5 mm/s | 0.162876 mm | 1.4 |
| 2 | 11–20 | 5 mm/s | 5 mm/s | 0.162876 mm | 1.4 |
| 3 | 21–30 | 5 mm/s | 7.5 mm/s | 0.162876 mm | 1.4 |
| 4 | 31–40 | 5 mm/s | 10 mm/s | 0.162876 mm | 1.4 |
| 5 | 41–50 | 5 mm/s | 5 mm/s | 0.15 mm | 1.4 |

The user explicitly selected keeping flow ratio 1.4 for the nominal 0.15 mm row. These are calculated/commanded widths, not a guarantee of the measured physical bead width. Flow is included in E once; M221 stays at 100%. Rows 1–4 retain the dominant width used in the prior triangular file and successful slicer reference. All model first layers run at 5 mm/s, including the objects with different upper-layer speeds. The test varies speed and therefore volumetric deposition rate, while keeping the flow ratio at 1.4.

## Common settings

- Bambu Lab P1S, 0.2 mm nozzle, PETG.
- Nozzle 255°C; bed 70°C; full pressure-advance command `M900 K0.55 L1000 M10`.
- First-layer deposition acceleration 500 mm/s²; upper layers 2000 mm/s². Travel acceleration 10000 mm/s².
- XY purge-line extrusion moves at 20 mm/s. Stationary flushing, retraction and travel retain startup settings.
- Retraction 0.4 mm while wiping 2 mm backward along the existing straight outro; lift to Z1 before transferring.
- P1S cleaning, bed-leveling and vibration-check startup retained from `FZigZagSquare1.4.gcode`, with mesh bounds adapted and stale time/progress estimates removed. Startup cleaning temperatures and final cooldown are retained.
- Each triangular path is uniformly scaled from the original triangular matrix. Mirror baseline separation is increased by rigid translation where needed to keep the two straight baselines at least 1 mm apart. Neither the triangle angles nor their shape are changed by that translation. Adjacent roads within a triangle can merge at the smallest spacings.

## Part-cooling policy from FZigZag5mmS1.4.gcode

The supplied fan reference configures part cooling off for the first three layers of each object, fan minimum 40%, maximum 90%, fan-cooling layer time 30 seconds, and slowdown layer time 12 seconds. The emitted reference speeds show intermediate fan settings for larger objects rather than a fixed 90% on every object.

This file uses that same fan-versus-layer-time rule, calculated for each new mirrored pair and layer:

- Layers 1–3: part fan off.
- Layers 4–10: 90% for estimated layer times at or below 12 seconds, 40% at or above 30 seconds, and linear interpolation between those thresholds.
- Auxiliary fan remains off during model deposition. Startup fan behavior is retained.

Layer times are estimated from the commanded deposition, travel, Z, unretraction and wipe motions. The timing estimator assumes rest-to-rest acceleration for each segment for timing purposes only; it inserts no pauses or stops. It is an approximation, not OrcaSlicer's exact firmware/timing simulation. Because these objects contain two paths and long tails, their estimated layer times and resulting fan PWM differ from a single-path slicer object. Exact per-layer PWM values and time estimates are in the CSV; the SVG shows approximate upper-layer percentages. No layer-time slowdown is allowed to override the requested printing speeds.

## Verification

Independent replay checked all 46,000 deposition moves: 500 layer events and 1000 path passes. Checks cover every first-layer speed, all upper-layer speeds, E per distance, nozzle/bed/K, acceleration, fan PWM, Z and travel clearance. Every object repeats identical XY and E across all ten layers. All rows reuse the same size geometries. Paths fit the plate with no overlap between separate pair envelopes. Nominal path envelope including 0.15 mm margin: X23.15–235.20, Y13.85–242.15 mm.

The SVG and PNG show the actual nozzle centerlines, numbered objects, sizes, speeds, nominal widths, flow ratios and fan settings. These are static checks; this new combination has not been physically printer-tested.
