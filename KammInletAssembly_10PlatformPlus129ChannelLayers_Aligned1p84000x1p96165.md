# Kamm inlet assembly: 70°C bed, off-part transition wait, wall-attached roof

This updates the existing assembly artifacts under their existing filenames. The first ten platform layers and their startup are unchanged. Both channels still contain 129 layers, interleaved left/right at each height, for 139 physical layers and an 8.34 mm final model height. The inlet alignment is unchanged.

## Bed temperature and transition parking

The bed remains at 70°C throughout platform and channel printing. The source channels' 85°C bed setting is deliberately overridden. There is no bed-temperature wait after the platform.

After platform layer 10, while already retracted, the nozzle lifts to Z5 and moves to X20/Y220. M400 completes that parking move before the nozzle-temperature wait for 245°C. This is well away from the model footprint around X124–132/Y115–141. It does not hover over or touch the print during cooldown. The transition repeats no startup, homing, calibration or purging. Normal heater shutdown remains at the end.

## Why the original roof failed

The uploaded channel files label their first roof island as `Overhang wall`. At source layer 7 (physical layer 17, Z1.02 mm), they start a narrow closed loop near the middle of the channel before printing the supported surrounding walls. In the left source, that loop lies between X128.086 and X128.290, spanning Y119.946–132.256. Its roads have no contact with the previous-layer side walls; the first island runs at 10 mm/s.

The working `cantilver_PETG_9m25s.gcode` and `LongOVERHANG2_PETG_16m19s.gcode` emit actual `WAVE_OVERHANG_START` blocks: slow parallel bands built progressively from an existing boundary, using 2 mm/s and full part cooling. They use a 0.4 mm nozzle and 0.2 mm layers, with 0.35 mm lateral spacing and a larger volumetric bead. Those absolute dimensions/flow amounts are unsuitable for this assembly's 0.2 mm nozzle and 0.06 mm layers; the boundary-first method is adapted instead.

## New wall-attached wave generation

Only the detached first island of source layer 7 is replaced on each channel. The supported circular/normal perimeters and scarf wall contours in that layer are retained and printed first. The orphaned initial helical travel that belonged to the removed island is omitted; the layer-entry wrapper already provides a safe lift.

The repair then prints three continuous longitudinal bands, alternating direction. Short lateral transfers between adjacent bands do not extrude, following the successful long-overhang example's method. There are no fan-settling dwells or pauses over the part.

- Deposition speed: 2 mm/s.
- Part fan: PWM255 (100%) during the new bands, then restore the normal PWM229 state.
- Deposition acceleration: 2500 mm/s², as in the working references.
- Nominal wave width: 0.217056 mm, retained from the removed source overhang feature.
- Layer height: 0.06 mm; flow ratio 0.98 included in E once. E is calculated for actual path length and this bead area; the 0.4 mm references' much larger absolute extrusion is not copied.
- Lateral spacing: approximately 0.163795 mm, below the calculated road width. The first road overlaps the already printed wall, each next road overlaps the preceding road, and the last overlaps the opposite printed wall.
- The current supporting wall also overlaps the previous layer, giving a continuous support chain from earlier material rather than a free-standing central start.

For the left channel in its original source coordinate frame, the supporting wall is X127.840 and the opposite wall X128.535. New band centers are X128.003795, X128.167590 and X128.331386, each spanning Y119.946–132.256. The right member uses the corresponding opposite direction from its printed wall, at source X127.996205, X127.832410 and X127.668614. Assembly translations are then applied unchanged.

Using the same rounded-rectangle bead-volume model as the extrusion calculation, the estimated contact overlaps are approximately 0.0898 mm against the starting wall, 0.0492 mm between adjacent roads and 0.0500 mm against the far wall. These are geometric/volume-model checks, not measurements or guarantees of physical bonding. The roof adds material to connect the formerly detached island to the walls; it is a deliberate local change to the roof generation, not an unchanged copy of that source island.

Each new roof finishes with a 0.4 mm retraction over a 2 mm wipe along the printed final band. Original normal-contour wipes are retained before the wave. The source extruder retracted/unretracted state remains balanced across channel changes. No arbitrary internal segmentation is added: each approximately 12.31 mm band is one deposition move.

All other source channel layers retain their deposited paths, E values, F values, acceleration, variable-width/scarf behavior and fan states. The only global source-profile override is the requested 70°C bed temperature. Normal channel printing remains 245°C nozzle, K0.05, source flow 0.98, 3 mm/s on source layer 1 and 5 mm/s on ordinary later paths. The existing platform settings remain 255°C/70°C/K0.55 with its original flow and speeds.

## Unchanged alignment

The lower-left inlet center remains 1.84000 mm right of the bottom inlet platform's outer left vertical centerline and 1.96165 mm above its lowest horizontal centerline. Those reference lines are X124.420016 and Y114.710299.

- Left inlet center: X126.260016, Y116.671949.
- Right inlet center: X129.739984, Y116.671949, mirrored about X128.

Centers are fitted to the supplied rounded first-layer ring toolpaths, not supplied analytic CAD circles. The original circle-fit reference and rigid XY translations are retained. No scaling is applied to either channel.

## Schematic and verification

The updated SVG/PNG retains the full assembly, inlet alignment detail and Z stack. It adds a large before/after wave panel showing previous walls and detached roads, followed by printed walls and numbered bands with direction arrows. The band footprints use the calculated extrusion model and are explicitly labeled as unmeasured material.

Final replay checks all output deposition XYZ/E/F, bed/nozzle/K, acceleration and fan states. Platform startup and the first ten printing layers are independently compared verbatim. Every unmodified channel layer is checked against its uploaded source; supported normal contours of the repaired layer retain their original deposition commands before the new wave. Tests verify supporting-wall coverage, positive band overlaps, the single off-part nozzle-temperature wait, no post-platform bed wait, no heating above 70°C before shutdown, layer count, alignment and mesh coverage.

The CSV records the revised layer-7 speed/fan ranges and wave-band count. The validation JSON records the repair coordinates and overlap calculations. Static checks passed; the revised overhang has not been physically printed and needs a test to establish bonding, dimensional quality and channel clearance.
