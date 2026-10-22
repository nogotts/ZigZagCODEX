# Revised square-wave matrix: 255 C and Orca motion settings

Start with `SquareWave_Matrix_Coalesced_255C_OrcaMotion_Check05_10.gcode`. It prints original IDs 05-10 only: 0.3, 0.4 and 0.5 mm step spacings, each at 0% and 50% upper-layer fan. These are the sizes reported to show poor upper-layer deposition. The full job prints all 60 original pairs, at the same positions shown in the updated SVG.

## Changes

- Print nozzle target: 255 C, matching both uploaded square-wave slicer references. Startup common flush is 250 C, pre-wipe cooldown 235 C, and the 140 C cleaning stage is preserved.
- First-layer print acceleration remains 500 mm/s^2; all upper-layer print acceleration is now 2000 mm/s^2, matching the emitted M204 settings in both references.
- Retraction is now distributed along a 2 mm backward wipe on the existing 10 mm outro, at F600, then the nozzle lifts to Z1.00. This follows the references' 0.4 mm retraction/2 mm wipe pattern without touching the square-wave region.
- Added two-second fan-settling waits are removed. Fan conditions remain explicit, and layer-transition actions occur after lifting from the previous print.

## Preserved

Every positive deposited XY/E/F command is identical to the prior coalesced file. The 90-degree geometry, all 45 deposited moves per path, exact extrusion totals, line width 0.15 mm, 0.06 mm layers, ten layers, 10 mm/s first layers, 15 mm/s upper layers, 85 C bed, 0/50% upper cooling, 20 mm/s purge, and original placements are preserved. Startup/calibration and shutdown are retained, except the documented thermal targets.

These files intentionally retain fixed 0.15 mm commanded width, unlike the slicer references' variable Arachne widths; they do not claim equal bead volume to those wider roads. No unmeasured pressure-advance value has been inserted.

## Validation

The full job was replayed against every original path: all 1,200 deposited path passes have exact matching XY/E/F sequences, with only axis-aligned edges. All 54,000 deposition commands have the required nozzle/bed target, fan, layer height and active acceleration. All 1,200 end wipes remain inside their existing outro lines. No fan-settling dwell or retract interrupts a deposited path. Startup and end routines remain present. The short check was independently verified as the exact selected subset with corrected layer notifications. SVG is well-formed XML and the CSV settings key is updated.

This is static verification, not physical print validation. A successful sample print is required before treating the deposition/bonding problem as resolved. If the check still produces weak or discontinuous roads, the remaining differences to investigate include the fixed narrow bead versus Orca's wider Arachne deposition, physical flow calibration and active pressure-advance calibration. A full matrix run is not needed to establish that result.
