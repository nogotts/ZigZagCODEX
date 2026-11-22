# KammInletH: scaffold, channel intros and extended horizontal lines

The existing filenames are retained. There are sixteen physical layers: ten scaffold/platform layers followed by the first six source layers of each aligned inlet channel. Final printed height remains 0.960 mm. The filename's `10mmHorizontalLines` describes the base-layer roads; channel-layer roads are now longer.

## Current layer sequence

Base layers 1–10 are unchanged: left scaffold → left bottom horizontal pair → left top pair → right scaffold → right bottom pair → right top pair → left angled stroke → right angled stroke. Each base layer retains eight 10 mm horizontal roads, with nominal width 0.30 mm, flow 1.4 and 0.15 mm pair pitch.

Channel layers 11–16 print: complete left channel loop → left 10 mm diagonal intro → complete right channel loop → right 10 mm diagonal intro → four extended left horizontal roads (bottom pair then top pair) → four extended right horizontal roads (bottom pair then top pair).

There are 128 horizontal deposition moves total: eighty unchanged 10 mm base roads, plus forty-eight extended channel-layer roads. Each extended road remains one uninterrupted straight deposition move, rather than a separate stop/start extension.

## Extended horizontals on layers 11–16

All original outer starting endpoints are fixed. Left roads begin at X113.920016 and run rightward; right roads begin at X142.079984 and run leftward. Their Y coordinates remain 116.521949,116.671949,139.326724 and139.476724 mm on both sides. Both roads in each pair remain 0.150 mm apart vertically.

Each channel-layer inner endpoint extends inward until its shortest XY distance to that layer's actual channel-wall nozzle path is 0.500 mm. This uses the established path-centerline gap convention, not a measured material-edge clearance. The supplied polygonal channel contours have slight layer-to-layer and side-to-side differences, so each road is solved against its own current contour. Full extended lengths range from 10.303286 to 10.321049 mm; none of the starting points moves inward.

| Side | Y, mm | Inner X at layer 16, mm | Full length, mm |
|---|---:|---:|---:|
| left | 116.521949 | 124.230316 | 10.310300 |
| left | 116.671949 | 124.223302 | 10.303286 |
| left | 139.326724 | 124.235436 | 10.315420 |
| left | 139.476724 | 124.227769 | 10.307753 |
| right | 116.521949 | 131.768631 | 10.311353 |
| right | 116.671949 | 131.762140 | 10.317844 |
| right | 139.326724 | 131.767515 | 10.312469 |
| right | 139.476724 | 131.761263 | 10.318721 |

All extended horizontals retain nominal width 0.30 mm, layer height 0.06 mm, flow ratio 1.4 included in E once, speed 25 mm/s and acceleration 2000 mm/s². E is recalculated from the actual full length using rounded-rectangle area `(width−height)×height + π×(height/2)²`, 1.75 mm filament and flow 1.4. E per path millimeter is 0.0100272683173; each longer road uses its own rounded E value. Width/flow declarations and actual extrusion both match the intended settings. Nominal width is not a measurement of printed bead width.

Each retained 0.4 mm retraction/wipe remains exactly 2 mm long, repositioned relative to the new inner endpoint. Primes, retraction amounts, speeds, travel lifts, fans, temperatures and K values are unchanged. The horizontal roads still print after both complete channel-loop/diagonal-intro pairs.

## Retained diagonals and channel registration

The first-ten-layer angled strokes remain unchanged: one 10 mm stroke on each side, nominal width 0.30 mm and flow 1.4. The left highlighted point is X124.035909/Y121.492244. The up 0.37793 → left 0.49614 → up 0.06202 reference sequence places the inner left endpoint at X123.539769/Y121.932194. The stroke points 7.125016° clockwise from left-to-right horizontal; the right stroke is its mirror.

The twelve channel-stage diagonal intros also remain unchanged. They are 10 mm windows on the same diagonal reference lines, shifted inward over the scaffold to stop 0.500 mm from their own channel-wall paths. Left intro: X115.520825/Y122.934562 → X125.443604/Y121.694215. Right intro: X140.474884/Y122.934026 → X130.552105/Y121.693678. Both use nominal width 0.30 mm, flow 1.4 and 25 mm/s. Their small along-line registration difference accounts for the supplied channel contours' tilt/chamfer differences while preserving the 0.500 mm gap.

The source channel geometry is retained from `KammInletChannel1_Left.gcode` and `ChannelRightNEw.gcode`, layers 1–6 only. Their original orientation, registered circular centers and +0.600 mm Z offset are unchanged. No source layer 7 or later, roof or wave-overhang stage is included. Source E, variable widths, 3/5 mm/s feedrates, acceleration, fan changes and scarf Z ramps remain unchanged.

## Temperatures, startup and transfers

The base uses 255°C nozzle, 70°C bed and K0.55; the channel stage uses 245°C nozzle, 70°C bed and K0.05. Added horizontal/diagonal roads retain flow 1.4; the original channel contours retain their own source flow 0.98 baked into E. M221 remains 100%.

The original P1S/0.2 mm-nozzle startup, purge and adaptive leveling rectangle remain unchanged. The nozzle-temperature transition waits at X20/Y220/Z5 with M400 completing the off-part park before M109. No additional thermal waits, K changes, fan commands or dwells are introduced by this update. Retraction/prime balances remain unchanged. Travel lifts remain at least 0.40 mm above the current nominal layer where specified by the existing added-road blocks. There is one startup, one object scope and one final shutdown; final height-dependent shutdown parks remain Z1.46, Z100.96 and Z98.96.

## Diagram and validation

The same SVG/PNG preserves the scaffold, channel, paired horizontal and diagonal geometry. Blue endpoint tips show the additional horizontal lengths on the top channel layer; the new lower key lists the extended lengths and emphasizes the fixed starting points. Earlier red diagonals identify the base strokes; dashed teal identifies the unchanged channel-stage diagonal intros.

Independent replay verified all 9386 non-horizontal deposition moves are unchanged, including every source channel loop and all diagonal intros. All eighty base horizontal deposition moves and the complete first-ten-layer executable prefix are unchanged. Each of the forty-eight extended roads is checked for its fixed start/Y, increased full length, 0.500 mm channel-path clearance, width, E per actual length, feedrate, acceleration, heater/K/fan state and 2 mm backward wipe. Checks retain the layer sequence, 128 horizontal deposition moves with no added segmentation, sixteen physical layers and 0.960 mm final model height.

These are static G-code checks; physical print quality has not been tested.
