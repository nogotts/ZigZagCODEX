# Filled zigzag with aligned mirrored channel: 10 + 5 layers

This new file in ZigZagCODEX prints the existing ten-layer filled zigzag, then adds five layers of the uploaded channel geometry aligned to it as shown in the supplied image. The original filled-zigzag file is not edited. Its startup and all ten executable base layers are copied verbatim into the new file; only the new header and added channel block differ. The existing shutdown is retained after the added block.

## Geometry and alignment

- Filled base: unchanged `FilledIn_ZigZag_0p6mm_10Layers_Obj68_25mms_K0p55_Flow1p4.gcode`, including its 0.6 mm mean same-side tip spacing, filled passes, mirrored positions, E amounts and bottom-endpoint starts.
- Channel: XY model geometry from `channel1_kamm.gcode`. Its generic startup, primer, temperatures, Z, E and ending commands are not imported.
- The source channel's longest right-hand vertical is 15.76827 mm. Uniform scaling by 0.963961170122 makes it exactly 15.200000 mm. Both X and Y scale together.
- On the left member, that longest vertical lies on the filled zigzag's right-side inner-tip baseline at X126.77. Its lower endpoint shares the filled path's bottom-start Y120.400474. Its top differs from the filled path's rounded-coordinate upper endpoint by only 0.000004 mm.
- The remaining channel runs left of that baseline, retaining the uploaded slight tilt of its inner long line, diagonals, short straight ends and rounded upper cap. This reproduces the reference-image placement.
- The complete channel is mirrored about X128 for the right member. The filled base was already mirrored about the same axis.
- Both new channel paths begin extrusion at their bottom endpoints on every added layer. The original base starts remain unchanged.

## Layer order and retained settings

| Layers | Geometry | Model Z | Deposition speed |
|---|---|---|---|
| 1 | Original filled base | 0.06 mm | 5 mm/s |
| 2–10 | Original filled base | 0.12–0.60 mm | 25 mm/s |
| 11–15 | New mirrored channel | 0.66–0.90 mm | 25 mm/s |

Layer height is 0.06 mm throughout, total height 0.90 mm. Each layer prints the left and right members before advancing to the next layer. The two-component assembly remains one object block.

Nominal width is 0.15 mm, flow ratio 1.4, K=0.55 with `M900 K0.55 L1000 M10`, nozzle 255°C and bed 70°C. The first ten layers retain their exact original settings. Added channel layers retain 2000 mm/s² deposition acceleration, part fan PWM227 (89.0%) and auxiliary fan off. E is calculated using actual straight/arc length and the original 0.004788797047574801 mm filament per path mm; flow is applied once and M221 remains 100%.

The startup's extruding XY purge line remains 20 mm/s. Added-channel transfer moves lift to Z1.30, keeping 0.40 mm above the final 0.90 mm object. Retraction is 0.4 mm while wiping 2 mm backward along the newly printed channel return line at 10 mm/s, followed by lifting. The existing mesh bounds already cover the entire new channel, so the original startup mesh command is unchanged.

## Segmentation and checks

The channel upload contains 671 sampled deposition moves. Collinear reduction and fitting of its existing rounded cap produce seven moves per mirrored side per layer: six straight G1 moves and one G2/G3 arc. Five channel layers therefore add only 70 deposition commands. There are no internal retractions, pauses or pressure changes within a channel path.

The validation JSON records hashes of the original base file and copied executable block. Checks verify byte-for-byte retention of the ten-layer base/startup, the 15.2 mm vertical dimension, alignment, complete mirroring, bottom-endpoint starts, fifteen-layer order, repeated channel XY/E, modal print settings, arc radius/length/E and coverage by the existing mesh envelope.

The SVG/PNG show the actual filled and channel centerlines together, with black highlighting the 15.2 mm return lines, blue highlighting the rest of the channel, green marking channel extrusion starts, and a side-view layer-stack diagram. These are static checks; physical print quality of the new stack remains unverified.
