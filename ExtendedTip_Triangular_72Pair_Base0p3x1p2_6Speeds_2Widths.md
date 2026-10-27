# Extended-tip triangular array: 72 mirrored pairs

This new file replaces the preceding triangular array's geometry while retaining its test combinations, print settings, layout and sequential object order.

## Exact new baseline geometry

For the left path, relative to one right-side inner tip A:

- A = (0, 0) mm.
- Left-facing outer tip B = (-1.2, 0.15) mm.
- Next right-side inner tip C = (0, 0.3) mm.

B is exactly 1.2 mm left of the midpoint of A–C, and 0.15 mm vertically from both A and C. The right path is the exact mirror. The baseline outward-tip angle is approximately 14.250 degrees. The previous 22-cycle count is retained, with analytical vertices rather than densely sampled collinear moves. Straight 10 mm intro/outro ends and mirrored baseline positions are retained.

As with the previous matrix, uniformly scale both triangle axes for the six test sizes:

| Same-side tip spacing | Horizontal reach from the inner baseline | Half-spacing |
|---|---|---|
| 0.5 mm | 2.0 mm | 0.25 mm |
| 0.6 mm | 2.4 mm | 0.30 mm |
| 0.7 mm | 2.8 mm | 0.35 mm |
| 0.8 mm | 3.2 mm | 0.40 mm |
| 0.9 mm | 3.6 mm | 0.45 mm |
| 1.0 mm | 4.0 mm | 0.50 mm |

The 0.3 mm / 1.2 mm dimensions define the unscaled reference, not an additional printed size. The SVG includes a dimensioned reference triangle and its mirror, as well as the full plate and numbered key.

## Same 72 combinations and settings

| Physical row (front to back) | Nominal width | IDs / layers 2–10 speed |
|---|---|---|
| 1 | 0.162876 mm | 01–06: 5; 07–12: 7.5; 13–18: 10 mm/s |
| 2 | 0.162876 mm | 19–24: 15; 25–30: 20; 31–36: 25 mm/s |
| 3 | 0.15 mm | 37–42: 5; 43–48: 7.5; 49–54: 10 mm/s |
| 4 | 0.15 mm | 55–60: 15; 61–66: 20; 67–72: 25 mm/s |

Sizes within each group increase left to right from 0.5 to 1.0 mm. Every object is a pair of mirrored paths, completed for all ten layers before moving to the next ID. Layer height is 0.06 mm; total height is 0.60 mm.

- Every first layer: 5 mm/s.
- Flow ratio: 1.4 everywhere, included once in E; M221 remains 100%.
- Pressure advance: `M900 K0.55 L1000 M10`.
- Nozzle 255°C; bed 70°C during all model deposition.
- Extruding XY purge-line moves: 20 mm/s. Startup cleaning temperatures and shutdown retained.
- First-layer deposition acceleration 500 mm/s²; upper layers 2000; travel 10000.
- Retraction 0.4 mm during a 2 mm wipe backward along the existing outro, then lift to Z1 before transferring.
- Part fan off layers 1–3, then the same 40–90% layer-time policy as the previous array: 40% at or above 30 seconds, 90% at or below 12 seconds, linear interpolation in between. The auxiliary fan is off during printing.

Longer paths require proportionally more E, calculated from their new lengths using the same width-specific E/mm and flow ratio. Their longer estimated layer times also change the fan PWM under the retained rule. The timing estimator includes movement, wipe and unretraction, using rest-to-rest acceleration for timing only; it inserts no stops. It is not an exact reproduction of OrcaSlicer's timing simulation. Nominal widths with flow 1.4 do not guarantee the measured physical bead widths.

## Verification

Independent replay validates 66,240 deposition moves, 720 layer events and 1,440 path passes. Checks include exact new tip dimensions and midpoint placement, mirror symmetry, same geometry across speed/width combinations, all first-layer and upper-layer speeds, temperatures, pressure advance, E per distance, cooling, Z and travel clearance. Each object's XY and E repeat on all ten layers. Every combination appears once, and all ten layers complete before the next object starts.

The new geometry fits the existing four-row layout without overlap between pair envelopes. Envelope including 0.15 mm margin: X20.825–242.700, Y23.850–231.150 mm. This new combination has not been physically printer-tested.
