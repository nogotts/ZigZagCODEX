# Five largest triangular zigzags, all layers at 5 mm/s

The user reports that `FZigZagSquare1.4.gcode` prints well. This new file uses the five largest distinct sizes from the original triangular matrix: 0.6, 0.7, 0.8, 0.9 and 1.0 mm tip spacing, ordered left to right. Each object contains two mirrored paths with 10 mm straight intro/outro sections, printed for ten layers before moving to the next object. These are triangular paths, not square waves.

## Measured differences from the old custom matrix

- The successful reference has filament flow ratio 1.4; the old custom code baked in 0.95. That difference alone raises commanded material by 47.4% at equal bead dimensions.
- The reference also uses Arachne widths of approximately 0.150–0.167 mm, rather than a fixed 0.150 mm. Its measured path-average filament extrusion is 0.005249812 mm per path mm, versus approximately 0.003249535 in the old custom matrix: 61.6% more material. Wider, fuller roads plausibly improve interlayer contact; this does not prove flow alone caused the failure.
- The reference uses 255°C nozzle and 70°C bed, versus 245°C/80°C in the latest custom square-wave matrix.
- Part cooling is off for layers 1–3 of each object, then PWM229 (approximately 90%), versus no part cooling throughout the custom speed matrix.
- It explicitly emits `M900 K0.55 L1000 M10`. The old custom version emitted only `M900 K0.5`. The firmware effect of the omitted parameters has not been established; the new file copies the full reference instruction.
- It uses 500 mm/s² acceleration for first-layer deposition and 2000 afterward. The latest custom square matrix used 2000 for every layer.
- It includes small Arachne corner transitions and variable widths. Those are not identical to ideal polygon corners. The new triangular file preserves the original triangle centerline geometry rather than importing square-wave corner geometry.

The successful reference prints first layers at 5 mm/s and upper layers at 10 mm/s. The new triangular file prints every model layer at 5 mm/s as requested. Actual improvement in this new combination has not been physically verified.

## Settings in the new file

- P1S, 0.2 mm nozzle, PETG; original reference startup, cleaning, bed leveling, vibration checks and shutdown retained. Adaptive mesh bounds changed for the new placement. Stale print-time estimates removed.
- Nozzle 255°C; bed 70°C; full pressure-advance instruction `M900 K0.55 L1000 M10`.
- Fixed commanded width 0.162876 mm, the dominant width in the reference, with flow ratio 1.4 baked into every deposited E value. M221 stays at 100%; the multiplier is not applied twice. This supplies 0.005238467421 mm filament per path mm, within approximately 0.22% of the reference's overall path-average amount. It does not reproduce Arachne's local width variation. Commanded width is not a promise of measured physical width, particularly with a 1.4 flow multiplier.
- Layer height 0.06 mm; ten layers; total height 0.60 mm. Identical XY and E repeated on all layers.
- Every model deposition move is 5 mm/s. All four extruding XY nozzle-load/purge-line moves are explicitly 20 mm/s. Startup stationary flushing and travel/retraction speeds retain the reference's settings.
- Part fan off layers 1–3, PWM229 layers 4–10; auxiliary fan off during printing.
- First-layer deposition acceleration 500 mm/s²; upper layers 2000; travel acceleration 10000 as used by the reference.
- Retraction 0.4 mm while wiping 2 mm backward along the existing straight outro, then lift to Z1 before travel.

## Verification

The independent replay checked all 5000 deposited moves: modal temperature, bed target, K, speed, acceleration, cooling, Z, and extrusion per distance. All 100 path passes repeat the expected geometry and E. Each path uses 50 moves, with collinear sampling removed to a maximum deviation below 0.00001 mm. Original triangle corners and 10 mm straight ends are retained. All paths fit the plate with clearance between objects. The SVG shows actual nozzle centerlines and the settings key. These are static checks, not a physical print guarantee.
