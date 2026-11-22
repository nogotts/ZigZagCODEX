# KammInletH: paired horizontal lines, scaffold diagonals and channel intros

This updates the existing G-code, SVG, PNG and validation JSON in place, without changing their filenames. The assembly remains ten platform layers followed by the first six layers of the uploaded left and right inlet files, for sixteen physical layers and a final printed height of 0.960 mm.

## Horizontal geometry and order

Every layer, including all six inlet layers, contains eight 10 mm horizontal lines. Each original line has one outward-offset copy: 0.150 mm below the original bottom line, or 0.150 mm above the original top line. The copies retain exactly the same X endpoints as their original lines. All right-side horizontal paths are exact mirrors about X128.

| Pair | First path Y, mm | Second path Y, mm |
|---|---:|---:|
| Bottom, both sides | 116.521949 (new outward copy) | 116.671949 (original alignment) |
| Top, both sides | 139.326724 (original alignment) | 139.476724 (new outward copy) |

Base layers 1–10 print in this order:

1. Complete the existing left scaffold.
2. Print the left bottom pair consecutively, outward copy first, then original alignment.
3. Print the left top pair consecutively, original alignment first, then outward copy.
4. Complete the existing right scaffold.
5. Print the mirrored right bottom pair consecutively.
6. Print the mirrored right top pair consecutively.
7. On layers 1–10 only, print the new left angled line, then its right-side mirror, after all eight horizontal lines are complete.
8. Continue through base layer 10. The channel-stage order is described below.

Left lines run left to right, from X113.920016 to X123.920016. Right lines run right to left, from X142.079984 to X132.079984. Each remains exactly 10 mm long. The gap from the inner horizontal endpoint to the platform outer vertical reference remains 0.500 mm centerline to centerline. Adjacent paired paths are 0.150 mm apart center to center.

## Added angled strokes on layers 1–10

The clarified highlighted-point construction is: up 0.37793 mm, left 0.49614 mm, then up another 0.06202 mm. The highlighted point is the lower endpoint of the longest outer left vertical platform segment, X124.035909/Y121.492244. This continuous reference sequence locates the inner/right endpoint of the left printed stroke at X123.539769/Y121.932194. The offset sequence is shown as dashed construction geometry in the SVG; the solid red line is the actual added deposition path.

Each new printed stroke is 10.000 mm long. For the left stroke, the outward endpoint is X113.616990/Y123.172541, and deposition travels inward to X123.539769/Y121.932194. Its direction from left to right is 7.125016° clockwise from horizontal. The right stroke is the exact reflection about X128: from X142.383010/Y123.172541 inward to X132.460231/Y121.932194. The mirrored highlighted point is X131.964091/Y121.492244.

The explicit supplied offsets put the inner endpoint 0.49614 mm horizontally from the long vertical centerline, rather than exactly 0.50000 mm. The explicit dimensions are retained without a further shift. Coordinate output is rounded to six decimals, giving less than 0.000002 mm length error and less than 0.00001° angle error.

There is one added stroke per side on each of the first ten layers: twenty new deposition moves total. They use nominal width 0.30 mm, layer height 0.06 mm, flow ratio 1.4 baked into E, and E0.10027268 per 10 mm stroke. Layer 1 runs at 5 mm/s and acceleration 500 mm/s²; layers 2–10 run at 25 mm/s and acceleration 2000 mm/s². These strokes inherit the base's 255°C nozzle, 70°C bed, K0.55 and layer-specific fan state. No angled strokes are added to layers 11–16.

Each pair runs after both structures and all eight horizontal lines have completed for that layer. Retracted, lifted approaches use corridors outside the existing feature footprint: above the model to reach the left stroke, below the model to switch to the right stroke, and outside the right-hand lines to return. Each stroke is one uninterrupted deposition move, followed by a 0.4 mm retract during a 2 mm backward wipe. The nozzle stays at Z1.00 during these transfers on layers 1–10, at least 0.40 mm above the current nominal layer. The added block restores the original XYZ, feedrate, acceleration and width state before the next original command. No new heater, K, fan or dwell commands are added.

## Channel-loop diagonal intros on layers 11–16

Each of the six channel layers now prints the complete original left channel loop, one new left diagonal intro, the complete original right loop, and one new right diagonal intro. The eight retained horizontal lines then print, left bottom/top pairs followed by right bottom/top pairs. There are twelve new channel intro deposition strokes. The first ten executable layers, including all scaffold paths, horizontal pairs and earlier red diagonal strokes, are unchanged.

Each added stroke is 10 mm long and lies on the exact infinite line of the earlier 7.125016° diagonal intro, or its right-side reflection. Its 10 mm window shifts inward: the stroke continues over the original zigzag scaffold's outer rail toward the channel. Deposition travels from the outside toward the channel. The inner endpoint has a 0.500 mm shortest XY gap to its own outer channel-wall nozzle path, using the existing path-centerline convention rather than an assumed measured bead edge.

- Left stroke: X115.520825/Y122.934562 → X125.443604/Y121.694215.
- Right stroke: X140.474884/Y122.934026 → X130.552105/Y121.693678.

The source left lower rail is very slightly tilted; its location at the new endpoint height is interpolated to compute the gap. The source right lower rail ends in a short chamfer, so its nearest endpoint is used for the 0.500 mm clearance. The supplied left/right toolpaths are not exact vertex-for-vertex reflections: the two new intro strokes have mirrored angles and length, with a roughly 0.0043 mm along-line registration difference so both clear their actual channel boundaries by 0.500 mm. They remain exactly collinear with the corresponding pre-existing diagonal paths.

New channel intro extrusion follows the existing diagonal-line settings: nominal width 0.30 mm, height 0.06 mm, flow 1.4 baked into E, E0.10027268 for each 10 mm stroke, speed 25 mm/s and acceleration 2000 mm/s². They inherit the channel stage's 245°C nozzle, 70°C bed, K0.05 and current fan state. The original channel contours keep their own source E values, flow 0.98, variable widths and 3/5 mm/s feedrates.

Each source loop's original final wipe/retraction is retained. The intro is approached while retracted at nominal layer Z +0.40 mm, primed 0.4 mm, deposited in one straight move, then retracted 0.4 mm during a 2 mm wipe back along the new road. Lifted transfers use the outside of the scaffold and an above-part corridor where practical. The complete right loop begins only after the left intro finishes. There are no added thermal waits, fan changes, K changes, or dwells.

## Horizontal extrusion settings

All eight horizontal paths on all sixteen layers use nominal width 0.300 mm, layer height 0.060 mm, and the horizontal lines' existing flow ratio 1.4. The flow ratio is baked into E once; M221 remains 100%. Layer 1 runs at 5 mm/s and acceleration 500 mm/s²; horizontal lines on layers 2–16 run at 25 mm/s and acceleration 2000 mm/s². Original horizontal speeds on platform layers 1–10 are retained, and that schedule continues through layer 16.

Extrusion is recalculated using the rounded-rectangle bead area `(width − height) × height + π × (height/2)²`, 1.75 mm filament, and flow ratio 1.4. Each uninterrupted 10 mm deposition move now uses E0.10027268. The original 0.15 mm horizontal paths used E0.04788797; their extrusion has been increased along with the width declaration. There are 128 horizontal deposition moves, totaling 1280 mm of path. Nominal width and calculated bead volume are not measurements of physical printed width.

Horizontal paths inherit the current stage's temperature, K and fan state: platform layers use 255°C nozzle, 70°C bed and K0.55; the six inlet layers use 245°C nozzle, 70°C bed and K0.05. Horizontal flow remains 1.4 throughout, while the original inlet paths retain their source flow 0.98 and original E values. The structure/inlet feedrate, acceleration and width state are restored after each four-line side group.

## Transfers

The original structure's final retraction/wipe completes before the horizontal paths. Each horizontal line is approached while retracted, lowered to its nominal layer height, primed by 0.4 mm, and printed in one move. It ends with a 0.4 mm retraction during a 2 mm backward wipe along the line and then lifts again.

Travel height is `max(1.00 mm, current nominal layer Z + 0.40 mm)`: Z1.00 for the first ten layers and Z1.06–1.36 for the six inlet layers. Transfers between the four horizontal lines remain on the outside of their structure. The two bottom paths finish before transfer to the top pair; all left paths finish before the original right structure/inlet is printed. The full part and added lines fit the existing adaptive leveling rectangle.

## Retained structure and inlet settings

All original channel/scaffold executable deposition commands are retained, including the original platform and inlet geometry, E values, F values, arc I/J values, scarf Z ramps, fans, acceleration, heaters and K values. The original startup, purge, widened leveling region, inlet alignment, and final shutdown are retained. The off-part transition wait remains at X20/Y220/Z5 before the nozzle changes to 245°C, and the bed remains 70°C. There is still one startup, one object scope, and one shutdown.

The inlet source files remain `KammInletChannel1_Left.gcode` and `ChannelRightNEw.gcode`, layers 1–6 only. They retain their original orientation and rigid XY translation to the existing circular centers, with Z offset +0.600 mm. The first inlet layer runs at 3 mm/s and the following five at 5 mm/s. No source layer 7 or later, roof, or wave-overhang stage is printed. Final shutdown height-dependent parks remain Z1.46, then Z100.96 and Z98.96.

## Diagram and validation

The same SVG/PNG retains the original platform and inlet geometry, horizontal pairs and highlighted-point detail. Dashed teal strokes show the new channel-stage intros continuing along the earlier red diagonals and over the scaffold. A new lower key lists the exact left/right intro endpoints, the gap convention and the channel-layer print order.

Independent replay verifies that all 9374 pre-existing non-horizontal deposition moves retain identical XYZ, E, arc I/J, F, width, acceleration, fans, heaters and K. All 128 retained horizontal deposition moves also retain identical states; only their placement in the six channel layers' sequence changes. The first ten executable layers are byte-for-byte unchanged. The twelve new intro strokes are independently checked for 10 mm length, collinearity with the earlier diagonal reference paths, 0.500 mm shortest distance to the source outer wall segment, scaffold-rail crossing, nominal 0.30 mm width and recalculated E, speed and temperature/K state. Checks also confirm the loop/intro ordering, balanced new retractions, lifted XY transfers, original off-part wait, sixteen layers, and retained 0.96 mm final model height.

These are static G-code checks; physical print quality has not been tested.
