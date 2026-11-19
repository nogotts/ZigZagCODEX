# KammInletH: paired horizontal lines and mirrored angled lines

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
7. On layers 1–10 only, print the new left angled line, then its right-side mirror, after all eight horizontal lines are complete.
8. Continue to the next layer, through layer 16.

Left lines run left to right, from X113.920016 to X123.920016. Right lines run right to left, from X142.079984 to X132.079984. Each remains exactly 10 mm long. The gap from the inner horizontal endpoint to the platform outer vertical reference remains 0.500 mm centerline to centerline. Adjacent paired paths are 0.150 mm apart center to center.

## Added angled strokes on layers 1–10

The clarified highlighted-point construction is: up 0.37793 mm, left 0.49614 mm, then up another 0.06202 mm. The highlighted point is the lower endpoint of the longest outer left vertical platform segment, X124.035909/Y121.492244. This continuous reference sequence locates the inner/right endpoint of the left printed stroke at X123.539769/Y121.932194. The offset sequence is shown as dashed construction geometry in the SVG; the solid red line is the actual added deposition path.

Each new printed stroke is 10.000 mm long. For the left stroke, the outward endpoint is X113.616990/Y123.172541, and deposition travels inward to X123.539769/Y121.932194. Its direction from left to right is 7.125016° clockwise from horizontal. The right stroke is the exact reflection about X128: from X142.383010/Y123.172541 inward to X132.460231/Y121.932194. The mirrored highlighted point is X131.964091/Y121.492244.

The explicit supplied offsets put the inner endpoint 0.49614 mm horizontally from the long vertical centerline, rather than exactly 0.50000 mm. The explicit dimensions are retained without a further shift. Coordinate output is rounded to six decimals, giving less than 0.000002 mm length error and less than 0.00001° angle error.

There is one added stroke per side on each of the first ten layers: twenty new deposition moves total. They use nominal width 0.30 mm, layer height 0.06 mm, flow ratio 1.4 baked into E, and E0.10027268 per 10 mm stroke. Layer 1 runs at 5 mm/s and acceleration 500 mm/s²; layers 2–10 run at 25 mm/s and acceleration 2000 mm/s². These strokes inherit the base's 255°C nozzle, 70°C bed, K0.55 and layer-specific fan state. No angled strokes are added to layers 11–16.

Each pair runs after both structures and all eight horizontal lines have completed for that layer. Retracted, lifted approaches use corridors outside the existing feature footprint: above the model to reach the left stroke, below the model to switch to the right stroke, and outside the right-hand lines to return. Each stroke is one uninterrupted deposition move, followed by a 0.4 mm retract during a 2 mm backward wipe. The nozzle stays at Z1.00 during these transfers on layers 1–10, at least 0.40 mm above the current nominal layer. The added block restores the original XYZ, feedrate, acceleration and width state before the next original command. No new heater, K, fan or dwell commands are added.

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

The same SVG and PNG show all eight horizontal paths and the two mirrored angled paths. The enlarged lower panel shows the highlighted point, the three up/left/up reference legs and the new inner endpoint. Light shading on printed strokes indicates the nominal 0.30 mm width. Blue/purple show the platform and magenta shows the top inlet contours. The diagram key lists the first-ten-layer angled-line step after the original eight-line sequence.

Independent replay verifies that all 9482 previously existing deposition moves, including all 128 horizontal roads, retain identical XYZ, E, arc I/J, F, width, acceleration, fan, heater and K state. Removing the new angled blocks reproduces the previous executable text exactly. Each new block restores its original modal and XYZ exit state, balances its primes/retractions, and adds only two 10 mm deposition strokes. Checks verify the twenty new strokes' explicit endpoint offsets, length, clockwise angle, nominal 0.30 mm width, E amount, mirror symmetry, first-ten-layer restriction, travel lift heights and mesh coverage. Sixteen physical layers, the unchanged inlet stage and final 0.96 mm printed height are retained.

These are static G-code checks; physical print quality has not been tested.
