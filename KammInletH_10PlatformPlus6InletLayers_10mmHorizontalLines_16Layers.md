# KammInletH: corrected circular-region clearance

The working files were restored from `ec863ddf3680f737805474567ada4ef695fae35f`, the version before the last horizontal-extension change. The correction below is applied to that baseline. Existing filenames are retained. The incorrect reference to channel-wall nozzle paths in commit `e0e7bef` is superseded.

## Correct clearance reference

The horizontal endpoints on layers 11–16 now lie **0.500 mm from the nominal outer circumferences of the circular inlet regions**, using the previously specified **3.29 mm outer diameter** and the existing registered inlet centers. Clearance is the shortest XY distance from the horizontal nozzle-centerline endpoint to that nominal circle circumference. It is not measured to a channel-wall nozzle path, circle center, scaffold edge, or assumed measured printed-bead tip.

The endpoint calculation is `distance(endpoint, circle center) = 3.29/2 + 0.500 = 2.145 mm`. For a horizontal line at Y, left endpoint X is `circle center X − sqrt(2.145² − (Y − circle center Y)²)`. The right endpoint uses the positive root. Coordinates are rounded to six decimals; independently checked clearances differ from 0.500 mm by less than 0.000001 mm.

The nominal circle dimensions and registered centers are reference geometry only. No channel contour is rescaled or otherwise modified. They do not claim a measured physical extrusion boundary.

## Horizontal paths

Original outer starting points remain fixed: left X113.920016, right X142.079984. Original Y values remain 116.521949, 116.671949, 139.326724 and 139.476724 mm on each side. Each pair retains its 0.150 mm vertical spacing. The eight base-layer roads on layers 1–10 remain exactly 10 mm, with the entire first-ten-layer executable prefix unchanged.

On layers 11–16, all eight roads extend inward to the corrected circular boundary reference. They are approximately **10.192139–10.203271 mm** long. Each remains a single uninterrupted deposition move from its original outer start. The geometry is repeated identically through the six channel layers.

| Side | Y, mm | Correct inner X, mm | Full length, mm |
|---|---:|---:|---:|
| left | 116.521949 | 124.120267 | 10.200251 |
| left | 116.671949 | 124.115016 | 10.195000 |
| left | 139.326724 | 124.112155 | 10.192139 |
| left | 139.476724 | 124.117399 | 10.197383 |
| right | 116.521949 | 131.879733 | 10.200251 |
| right | 116.671949 | 131.884984 | 10.195000 |
| right | 139.326724 | 131.881959 | 10.198025 |
| right | 139.476724 | 131.876713 | 10.203271 |

Extended horizontal settings remain nominal width 0.30 mm, layer height 0.06 mm, flow ratio 1.4 baked into E, speed 25 mm/s and acceleration 2000 mm/s². Filament diameter remains 1.75 mm and M221 remains 100%. E is recalculated from the full new line length using `(width−height)×height + π×(height/2)²`, divided by filament cross-sectional area and multiplied by flow 1.4. Two-millimeter backward wipes are repositioned relative to the corrected endpoints; prime/retraction amounts remain ±0.4 mm.

## Retained order and settings

Base layers 1–10 are unchanged, including both scaffolds, horizontal pairs and the earlier angled lines. On channel layers 11–16 the sequence remains complete left channel loop → left diagonal intro → complete right channel loop → right diagonal intro → left bottom/top horizontal pairs → right bottom/top horizontal pairs.

All twelve channel-stage diagonal intros remain unchanged: 10 mm long and collinear with the earlier scaffold diagonals, crossing the scaffold toward their own channel-wall paths. The supplied source channel loops retain their original E, F, variable widths, acceleration, scarf Z ramps, fans and registered positions. Only source channel layers 1–6 are included; no roof stage is printed. The total remains sixteen layers and 0.960 mm printed height.

The existing startup, purge, leveling area, off-part temperature wait, travel lifts and final shutdown remain unchanged. Base temperature/K remain 255°C nozzle, 70°C bed and K0.55; channel stage remains 245°C nozzle, 70°C bed and K0.05. Original channel flow 0.98 remains baked into its own E values, while added lines retain flow 1.4. There are no new heater, fan, K or dwell commands.

## Clear diagram and validation

The new SVG/PNG includes a full assembly overview plus four enlarged circle details. Solid purple circumferences show the nominal **3.29 mm circular-region outer boundaries**. Gray dots mark former 10 mm line endpoints; blue segments and dots show the corrected inward extensions and endpoints. Each detail explicitly dimensions **0.500 mm** between the endpoint and the circle boundary. The table gives all eight corrected endpoint coordinates and lengths.

Independent replay verified all 9386 non-horizontal deposition moves against the restored baseline, including every channel loop and diagonal intro. All eighty base horizontal roads and the complete first-ten-layer executable prefix are unchanged. Each of the forty-eight corrected channel horizontal roads retains its outer start, Y, width, speed, fan, temperature and K state; E matches full length; the endpoint has the required circle-boundary clearance; and each backward wipe remains 2 mm. Workflow, sixteen-layer count and no added horizontal segmentation are verified. Validation details are recorded in the JSON.

These are static G-code and nominal-geometry checks; physical print quality has not been tested.
