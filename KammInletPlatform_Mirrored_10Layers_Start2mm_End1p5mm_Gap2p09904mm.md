# Kamm inlet platform: mirrored, 10 layers, 2 mm start and 1.5 mm finish

This is a new geometry-only replacement job using the print settings from `FilledInZigZag_ChannelStack_10plus5Layers_0p6mm_Channel15p2mm_Obj68.gcode`. Existing repository files are not overwritten. Only the model XY path from the uploaded `KammInletPlatform.gcode` is imported; its generic startup, primer, Z, E, temperatures and ending code are excluded. The new job prints this inlet-platform geometry for ten layers, without the previous separate channel overlay.

## Scale and direction

The uploaded path starts on the slanted line and ends on the bottom open vertical. That final vertical measures 1.194309 mm in the source. Uniform XY scale 1.674608497465898 makes it exactly 2 mm and makes the opposite slanted line 1.5000065 mm, consistent with the requested 1.5 mm dimension within source coordinate precision.

The complete path is reversed, including the direction of each circular arc. Every layer on each side therefore starts at the lower endpoint of the 2 mm vertical, moves upward, follows every supplied filled pass and both inlet platforms continuously, and ends on the 1.5 mm slanted segment. The bottom inlet platform itself extends below this open starting endpoint; the designated start is the open vertical highlighted green in the SVG. The final slanted segment is highlighted red.

## Mirroring and gap

The left supplied shape is mirrored exactly about X128 to create the right member. The actual inward-facing triangular tip cluster is at source X1.740449; platform edges and short open-end stems extend farther inward and are not used as the tip reference.

After scaling and placement, inward triangle tip centerlines are X126.95048 and X129.04952, giving exactly 2.09904 mm separation. Corresponding tips have identical Y values. The wider inlet-platform edge centerlines are only 0.200000 mm apart. With deposited bead thickness, those platforms may touch; the requested triangle-tip gap is retained exactly. All stated XY dimensions are centerline dimensions, not a guarantee of physical free space.

The complete mirrored pair's centerline envelope is approximately 7.928182 × 26.579402 mm, centered at X128/Y128. The source is uniformly scaled in both axes, retaining all platform proportions and filled-path offsets.

## Retained print settings

- Bambu Lab P1S / 0.2 mm nozzle / PETG.
- Ten layers at 0.06 mm, total model height 0.60 mm.
- Layer 1: 5 mm/s; layers 2–10: 25 mm/s.
- Nominal line width 0.15 mm; flow ratio 1.4 included in E once; M221 remains 100%.
- E per path millimetre: 0.004788797047574801 mm filament. Arcs use their actual circular length.
- Pressure advance: `M900 K0.55 L1000 M10`.
- Nozzle 255°C; bed 70°C.
- Part fan: off layers 1–3, PWM226 layers 4–6, PWM227 layers 7–10. Auxiliary fan off during printing.
- Deposition acceleration: 500 mm/s² first layer, 2000 upper layers; transfer acceleration 10000.
- Extruding XY purge line: 20 mm/s. Startup cleaning, bed leveling, vibration checks and shutdown retained from the parent; adaptive mesh bounds updated for the taller geometry.
- Retract 0.4 mm while wiping 2 mm backward along the already printed tail at 10 mm/s, then lift to Z1 before transfer. The wipe follows the final slant and then the preceding vertical rather than extending beyond the model.

## Segmentation and verification

The upload has 5048 sampled deposition moves. Collinear simplification and fitting of genuine circular bends reduce the new path to 418 moves per side: 40 G2/G3 arcs and 378 G1 moves. Tiny curved segments whose arc substitution would exceed the 0.003 mm deviation limit retain their original chords. The fitted-curve deviation bound is below 0.002218 mm. No arbitrary fixed-distance subdivision is added, and all real corners are preserved.

Independent final-command replay checks every model move's speed, Z, temperature, bed, K, fan, acceleration and extrusion per actual straight/arc length, including arc direction after path reversal and mirroring. Every side on every layer starts with the 2 mm vertical and ends with the 1.5 mm slant. All ten layers repeat identical XY and E. Mirroring, tip-gap dimensions, four extruding purge-line moves at 20 mm/s, object-marker balance and plate clearance are checked. The validation JSON records measured dimensions and provenance.

The SVG and PNG show actual generated paths, highlighted start/end segments, the tip-gap dimension, platform-edge gap and complete print settings. Static validation passed; physical printing remains unverified.
