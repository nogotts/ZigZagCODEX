# Filled-in 0.6 mm zigzag: one mirrored object using object 68 settings

The user identified object 68 in `ExtendedTip_Triangular_72Pair_Base0p3x1p2_6Speeds_2Widths.gcode` as the successful setting. This new file prints one centered object containing the uploaded filled-in path and an exact mirrored mate, for ten layers. Only the uploaded file's XY model geometry is imported; its generic startup, primer, temperature, Z, E, fan and ending commands are not used.

## Settings copied from object 68

- P1S / 0.2 mm nozzle / PETG.
- Layer 1: 5 mm/s. Layers 2–10: 25 mm/s.
- Fixed nominal width 0.15 mm, flow ratio 1.4, filament diameter 1.75 mm. E/mm is 0.004788797047574801, matching object 68. The flow multiplier is included in E once; M221 stays at 100%.
- Full pressure command `M900 K0.55 L1000 M10`.
- Nozzle 255°C, bed 70°C; ten 0.06 mm layers, total height 0.60 mm.
- First-layer deposition acceleration 500 mm/s², upper layers 2000; transfer acceleration 10000.
- Exact object-68 fan schedule: layers 1–3 PWM0; layers 4–6 PWM226 (88.6%); layers 7–10 PWM227 (89.0%). This schedule is copied, not recalculated for the filled geometry's longer deposition time. Auxiliary fan remains off during the model.
- XY purge-line deposition speed 20 mm/s. P1S startup cleaning, bed leveling, vibration checks and shutdown retained from the parent, with adaptive mesh bounds updated for this centered object.
- Retraction 0.4 mm during a 2 mm wipe, then lift to Z1. The wipe follows the existing end of the new path backward (two straight moves), rather than projecting a 2 mm wipe beyond the attachment's short straight end.

## Geometry and scale

The uploaded `filledInZigZag0.6.gcode` contains one continuous filled zigzag: the sharp triangular boundary, the return filled pass with rounded turns, and a rounded outer pass, connected at the ends. All those passes and the uploaded short end sections are retained. The earlier matrix's separate 10 mm intro/outro lines are not added to this new geometry.

The actual uploaded same-side sharp-tip pitch averages 0.618389545455 mm, despite the nominal 0.6 mm filename. Uniform XY scaling by 0.970262198658 brings its average to 0.600000 mm. The tiny original coordinate variation remains: individual pitches are approximately 0.599992–0.600013 mm. Both X and Y scale together; the filled shape is not stretched in only one direction.

The single supplied path is placed as the left member, facing outward, then mirrored exactly around X128 to make the right member. Inner sharp-baseline separation is 2.46 mm, the same as parent object 68. The complete object is centered at X128/Y128.

Centerline dimensions after scaling:

- Sharp-boundary same-side pitch: 0.6000 mm mean.
- Sharp-boundary horizontal reach: approximately 2.4000 mm.
- Full filled single-path width: approximately 2.8000 mm.
- Complete mirrored pair width: approximately 8.0600 mm.
- Complete path height, including its short end sections/rounded turns: approximately 15.3940 mm.
- Sharp zigzag section span: 13.2000 mm.
- Model Z height: 0.6000 mm.

These are nozzle-centerline dimensions; deposited bead thickness adds to the physical outline. Nominal width with flow 1.4 does not guarantee the measured printed width.

## Avoiding excessive segmentation

The attachment uses 4340 deposited XY moves for its single filled path. Collinear simplification reduces that to 692. Circular fitting of the genuine rounded turns reduces the output further to 193 moves per filled path: 110 G1 straight moves and 83 G2/G3 circular arcs. These are XY arcs with relative I/J center offsets, using G17 and relative extrusion M83. No stop, retract or pressure command occurs inside either filled path.

The circular fits reproduce the original sampled curved polygon within 0.002508 mm maximum chord deviation after scaling (below the 0.003 mm validation limit). Straight triangle corners remain vertices. Every E amount is calculated using actual straight length or circular arc length at the same object-68 E/mm. Thus fitting does not reduce corner flow arbitrarily or reuse an E value from a segment of a different length.

The final job has 3860 model deposition commands across two paths and ten layers. Firmware still generates the motor steps required to execute arcs; reducing G-code commands does not remove that necessary internal interpolation.

## Validation and artifacts

Independent replay checks all G1/G2/G3 deposition speeds, temperatures, fan, K, acceleration, Z, radius consistency, signed arc sweeps and E amounts. All ten layers repeat identical XY and E. The mirror and uniform scale are checked. The object is within the plate, with transfers at Z1 above the 0.6 mm print. The JSON report includes provenance, dimensions and checks.

The main SVG/PNG is the settings key and complete top view. The `_Geometry.svg`/PNG adds full dimensions and an enlarged view of the actual filled passes. Static validation passed; physical printing of this new filled geometry remains unverified.
