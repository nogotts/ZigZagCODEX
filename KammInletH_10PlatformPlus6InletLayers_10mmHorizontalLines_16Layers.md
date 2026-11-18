# KammInletH: eight paired horizontal lines on all sixteen layers

This updates the existing G-code, SVG, PNG and validation JSON in place, without changing their filenames. The assembly remains ten platform layers followed by the first six layers of the uploaded left and right inlet files, for sixteen physical layers and a final printed height of 0.960 mm.

## Horizontal geometry and order

Every layer, including all six inlet layers, contains eight 10 mm horizontal lines. Each original line has one outward-offset copy: 0.150 mm below the original bottom line, or 0.150 mm above the original top line. The copies retain exactly the same X endpoints as their original lines. All right-side horizontal paths are exact mirrors about X128.

| Pair | First path Y, mm | Second path Y, mm |
|---|---:|---:|
| Bottom, both sides | 116.521949 (new outward copy) | 116.671949 (original alignment) |
| Top, both sides | 139.326724 (original alignment) | 139.476724 (new outward copy) |

Each layer prints in this order:

1. Complete the existing left structure: platform on layers 1–10, inlet on layers 11–16.
2. Print the left bottom pair consecutively, outward copy first, then original alignment.
3. Print the left top pair consecutively, original alignment first, then outward copy.
4. Complete the existing right structure or inlet.
5. Print the mirrored right bottom pair consecutively.
6. Print the mirrored right top pair consecutively.
7. Continue to the next layer, through layer 16.

Left lines run left to right, from X113.920016 to X123.920016. Right lines run right to left, from X142.079984 to X132.079984. Each remains exactly 10 mm long. The gap from the inner horizontal endpoint to the platform outer vertical reference remains 0.500 mm centerline to centerline. Adjacent paired paths are 0.150 mm apart center to center.

## Horizontal extrusion settings

All eight horizontal paths on all sixteen layers use nominal width 0.300 mm, layer height 0.060 mm, and the horizontal lines' existing flow ratio 1.4. The flow ratio is baked into E once; M221 remains 100%. Layer 1 runs at 5 mm/s and acceleration 500 mm/s²; horizontal lines on layers 2–16 run at 25 mm/s and acceleration 2000 mm/s². Original horizontal speeds on platform layers 1–10 are retained, and that schedule continues through layer 16.

Extrusion is recalculated using the rounded-rectangle bead area `(width − height) × height + π × (height/2)²`, 1.75 mm filament, and flow ratio 1.4. Each uninterrupted 10 mm deposition move now uses E0.10027268. The original 0.15 mm horizontal paths used E0.04788797; their extrusion has been increased along with the width declaration. There are 128 horizontal deposition moves, totaling 1280 mm of path. Nominal width and calculated bead volume are not measurements of physical printed width.

Horizontal paths inherit the current stage's temperature, K and fan state: platform layers use 255°C nozzle, 70°C bed and K0.55; the six inlet layers use 245°C nozzle, 70°C bed and K0.05. Horizontal flow remains 1.4 throughout, while the original inlet paths retain their source flow 0.98 and original E values. The structure/inlet feedrate, acceleration and width state are restored after each four-line side group.

## Transfers

The original structure's final retraction/wipe completes before the horizontal paths. Each horizontal line is approached while retracted, lowered to its nominal layer height, primed by 0.4 mm, and printed in one move. It ends with a 0.4 mm retraction during a 2 mm backward wipe along the line and then lifts again.

Travel height is `max(1.00 mm, current nominal layer Z + 0.40 mm)`: Z1.00 for the first ten layers and Z1.06–1.36 for the six inlet layers. Transfers between the four horizontal lines remain on the outside of their structure. The two bottom paths finish before transfer to the top pair; all left paths finish before the original right structure/inlet is printed. The full part and added lines fit the existing adaptive leveling rectangle.

## Retained structure and inlet settings

All non-horizontal executable lines are retained, including the original platform and inlet geometry, E values, F values, arc I/J values, scarf Z ramps, fans, acceleration, heaters and K values. The original startup, purge, widened leveling region, inlet alignment, and final shutdown are retained. The off-part transition wait remains at X20/Y220/Z5 before the nozzle changes to 245°C, and the bed remains 70°C. There is still one startup, one object scope, and one shutdown.

The inlet source files remain `KammInletChannel1_Left.gcode` and `ChannelRightNEw.gcode`, layers 1–6 only. They retain their original orientation and rigid XY translation to the existing circular centers, with Z offset +0.600 mm. The first inlet layer runs at 3 mm/s and the following five at 5 mm/s. No source layer 7 or later, roof, or wave-overhang stage is printed. Final shutdown height-dependent parks remain Z1.46, then Z100.96 and Z98.96.

## Diagram and validation

The SVG and PNG show all eight horizontal nozzle paths, their paired spacing and updated print order. Light shading indicates a nominal 0.30 mm footprint; orange and green centerlines identify the two mirrored sides. Blue/purple show the platform and magenta shows the top inlet contours.

Independent replay verified all 9354 original structure/inlet deposition moves retain their original XYZ, E, arc I/J, F, width, acceleration, fan, heater and K state. Stripping the old horizontal blocks from the prior file and the new blocks from the updated file leaves identical executable text. All 128 horizontal moves are exactly 10 mm, follow the required eight-line order on every layer, use the recalculated E and declared 0.30 mm width, and mirror correctly. Checks also verify pair spacing, balanced retract/prime amounts, safe travel heights, mesh coverage, the off-part wait, sixteen physical layers, and final deposition height 0.96 mm.

These are static G-code checks; physical print quality has not been tested.
