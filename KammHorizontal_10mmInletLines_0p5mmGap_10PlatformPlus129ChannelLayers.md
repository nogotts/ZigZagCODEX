# KammHorizontal: inlet-alignment roads on the first ten layers

New variant of the user's uploaded `KammInletAssembly_10PlatformPlus129ChannelLayers_Aligned1p84000x1p96165-1.gcode`. The existing assembly files are retained.

Each platform layer now prints in this order: the full original left structure, a lower 10 mm horizontal road from left to right, an upper 10 mm road from left to right, the full original right structure, and the two mirrored roads from right to left. This repeats for all ten platform layers. There are 40 added roads, totaling 400 mm of deposition path.

## Coordinates and alignment

The reference outer left vertical platform centerline is X124.420016. Both left roads begin at X113.920016 and finish at X123.920016, leaving a 0.500000 mm centerline gap to that reference. Both right roads begin at X142.079984 and finish at X132.079984, mirrored about X128 and leaving the same gap to X131.579984. These are path-centerline dimensions rather than measured deposited-edge clearances.

The lower road is at Y116.671949; the upper road is at Y139.326724. These Y coordinates come from least-squares circle fits to the original left channel's exposed first-layer inlet ring vertices. Ring polygon/rounding residuals are below 0.003 mm. The right roads are exact geometric mirrors and use the same Y coordinates; the original right channel itself is unchanged. The requested 3.29 mm outer-diameter circles are shown as alignment overlays in the SVG, not added to the platform G-code.

## Settings and transfer motions

New roads use the same platform settings: 0.15 mm nominal width, 0.06 mm layer height, flow ratio 1.4 included in E once, 1.75 mm filament, and K0.55. Each uninterrupted 10 mm deposition move uses E0.04788797. Layer 1 runs at 5 mm/s and acceleration 500 mm/s²; platform layers 2–10 run at 25 mm/s and acceleration 2000 mm/s². Platform temperatures remain 255°C nozzle and 70°C bed. The existing per-layer fan schedule is inherited without alteration.

The existing structure's retract/wipe completes before each added pair. Each road is approached while retracted at Z1.00, lowered to the current platform height, primed by 0.4 mm, and printed as one move. It ends with a 0.4 mm retraction during a 2 mm backward wipe along the road, followed by a lift to Z1.00. The lower-to-upper transfer remains outside the original platform footprint and does not traverse the first road except to leave its wiped endpoint. These are open-air transfers, not deposition connectors. No new dwells or heating waits are inserted.

The original startup is retained except that its adaptive bed-leveling rectangle is widened to include the new roads and a margin: X111.845016, Y112.560299, width32.309968, height30.879402. The original purge commands and speeds are unchanged.

## Channel stage and verification

All content from `BEGIN ALIGNED CHANNEL STAGE` through final shutdown is byte-for-byte identical to the uploaded source. Both channels still have 129 layers, interleaved at each height after the ten platform layers; there are 139 physical layers and an 8.34 mm final printed height. This includes the uploaded source's existing roof generation, off-part temperature-transition park, and 70°C bed setting.

Independent replay verified all 31,827 original deposition moves retain command type, endpoint XYZ, E, arc I/J, feedrate, acceleration, fan state, and thermal/K commands. All 40 added deposition moves are exactly 10 mm horizontally at their specified speed and layer height, and new retractions/primes balance. Stripping the insertion blocks and reversing the documented mesh expansion reproduces the original source text exactly. Added roads fit inside the widened mesh region. Validation details are in the associated JSON. Static checks do not establish physical print quality.
