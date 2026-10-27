# Triangular array: 72 individually completed mirrored pairs

Six nominal triangle tip spacings (0.5, 0.6, 0.7, 0.8, 0.9 and 1.0 mm), six upper-layer speeds (5, 7.5, 10, 15, 20 and 25 mm/s), and two nominal widths (0.162876 and 0.15 mm). Every combination appears once, for 72 objects. Each object contains two mirrored triangular paths, with the same geometry and 10 mm straight intro/outro sections as the previous triangular array.

Every first layer prints at 5 mm/s. Each object completes all ten layers before moving to the next object, including both mirrored paths at each layer. Layer height remains 0.06 mm, total height 0.60 mm. Objects print in numbered order, left to right, then to the next physical row farther back on the plate.

| Physical row (front to back) | Nominal width | IDs / layers 2–10 speed |
|---|---|---|
| 1 | 0.162876 mm | 01–06: 5; 07–12: 7.5; 13–18: 10 mm/s |
| 2 | 0.162876 mm | 19–24: 15; 25–30: 20; 31–36: 25 mm/s |
| 3 | 0.15 mm | 37–42: 5; 43–48: 7.5; 49–54: 10 mm/s |
| 4 | 0.15 mm | 55–60: 15; 61–66: 20; 67–72: 25 mm/s |

Within each six-object group, size increases left to right from 0.5 to 1.0 mm. Geometry is uniformly scaled from the original 0.3 mm triangular baseline, preserving the shapes used in the previous array. Mirror straight-baseline spacing remains at least 1 mm, using only rigid translation where required; each path's angles and shape remain unchanged.

## Settings

- Bambu Lab P1S / 0.2 mm nozzle / PETG.
- Filament flow ratio 1.4 on every deposited path, included in E once; M221 remains 100%.
- Full pressure-advance command `M900 K0.55 L1000 M10`.
- Nozzle 255°C; bed 70°C throughout model deposition.
- All first layers 5 mm/s; all subsequent layers at the object's assigned speed.
- All four extruding XY purge-line moves are 20 mm/s. Stationary flushing, retraction and travel use the retained startup settings.
- First-layer deposition acceleration 500 mm/s²; upper layers 2000 mm/s²; transfer acceleration 10000 mm/s².
- Retraction 0.4 mm during a 2 mm wipe backward on the existing straight outro, then lift to Z1 before transferring.
- Original P1S startup cleaning, bed leveling, vibration checks and shutdown retained from the successful slicer reference. Mesh bounds adapted to this layout; stale time/progress estimates removed.
- Commanded nominal widths with a 1.4 flow multiplier do not guarantee those measured physical bead widths.

## Retained fan method

As in the most recent triangular array, this uses the cooling policy from `FZigZag5mmS1.4.gcode`: part fan off on layers 1–3 of every object, then 40–90% according to estimated layer time. At or above 30 seconds, use 40%; at or below 12 seconds, use 90%; linearly interpolate between them. Auxiliary fan stays off during model deposition.

The estimator includes deposition, travel, Z moves, wipe and unretraction. It assumes rest-to-rest acceleration per segment for timing only, without inserting stops or waits. It is not OrcaSlicer's exact timing simulator. Cooling does not override the requested printing speeds. The key shows approximate lower upper-layer percentages; the CSV records exact PWM and estimated time for every layer of every object.

## Validation

Independent command replay validates 66,240 deposition moves, 720 layer events and 1,440 path passes: XY/E, first/upper speeds, Z, temperatures, pressure-advance K, acceleration and cooling. Every object repeats the same XY and E on all ten layers. All 72 size/width/speed combinations appear exactly once. All objects fit the plate, with no overlap between separate pair envelopes. Envelope including a 0.15 mm margin: X21.825–240.700, Y23.850–231.150 mm.

The SVG and PNG show actual nozzle centerlines and a complete numbered key. Static validation does not establish physical print quality; this new array remains unverified on the printer.
