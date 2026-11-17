# Kamm inlet assembly: unchanged ten-layer platform plus both complete channel files

This new assembly prints the existing `KammInletPlatform_Mirrored_10Layers_Start2mm_End1p5mm_Gap2p09904mm.gcode` platform for ten layers, then both uploaded channel models on top. Each uploaded channel contains 129 layers of 0.06 mm. They are interleaved left/right at every height, giving 139 physical layers and a final model height of 8.34 mm.

## Alignment references

The left inlet is aligned to the outer left vertical and lowest horizontal **centerlines of the bottom inlet platform rectangle**, not the farther-left zigzag rail. Those reference lines are X124.420016 and Y114.710299.

The lower inlet-circle center is placed 1.84000 mm to the right of the reference vertical and 1.96165 mm above the reference horizontal:

- Left center: X126.260016, Y116.671949.
- Right center: X129.739984, Y116.671949, the exact mirror position about X128.

The lower circle centers in the supplied G-code are recovered with a least-squares fit of the exposed first-layer inlet ring away from its stem junction. The left source fit is approximately (128.002435132, 114.671912412), and the right fit is (128.002510792, 114.671860894). Their fitted radii are approximately 1.536 mm. The source points are rounded slicer toolpaths with variable bead widths, not a supplied analytic CAD circle; these fitted centers are an alignment reference, not a promise of physical five-decimal manufacturing accuracy. The selected ring samples deviate from their fitted circle by roughly 0.0022 mm or less.

No XY scaling or toolpath regeneration is applied to either uploaded channel. Only rigid XY translation is applied:

| Source | X translation | Y translation |
|---|---:|---:|
| KammInletChannel1Try1.gcode | -1.742419132 mm | +2.000036588 mm |
| KammInletChannel1Try1Right.gcode | +1.737473208 mm | +2.000088106 mm |

The right upload is used for the right member as supplied. Its model is the mirrored channel, but its slicer seam positions, path subdivision and local widths differ slightly from the left upload; the right file is not replaced with a newly mirrored/resliced copy of the left. Its inlet center is placed at the mirrored reference coordinates while all its own deposition moves remain intact.

## Layer sequence and settings

| Stage | Physical layers | Model Z | Nozzle / bed | K | Source deposition speeds |
|---|---|---|---|---|---|
| Existing platform | 1–10 | 0.06–0.60 mm | 255°C / 70°C | 0.55 | 5 mm/s first; 25 mm/s afterward |
| Left + right channels | 11–139 | 0.66–8.34 mm nominal | 245°C / 85°C | 0.05 | 3 mm/s source first layer; 5 mm/s afterward |

The platform startup and all ten executable printing layers are copied verbatim. The original platform file is not modified. Its source geometry, E, speed, cooling, pressure advance and mesh remain unchanged.

After the platform, the head lifts and changes to the uploaded channels' temperature and pressure settings. It does not repeat homing, calibration, nozzle cleaning, purging or a separate startup. Each source Z coordinate is raised by exactly 0.60 mm; this includes the sources' scarf-seam Z ramps, which intentionally start slightly below a nominal layer height. Relative E values are preserved exactly, as are inline F values, variable line-width metadata, acceleration commands and deposition fan states.

The channels use their original flow ratio 0.98 already baked into their E commands; the platform's 1.4 multiplier is not applied to them. M221 stays at the uploaded files' 100% flow override. The full pressure command is `M900 K0.05 L1000 M10`. Chamber fan and auxiliary/part fan states are restored from each source's modal state, including any fan changes within source model bodies or before their wipes.

Each source's original priming/unretraction and wipe moves are retained. The initial startup retraction from the uploaded files is not repeated because the completed platform has already retracted; repeating it would double-retract before the first channel. Subsequent layer transfers lift vertically to 0.4 mm above the nominal current channel height before moving between the two members. Source deposition and internal scarf/travel moves remain translated copies. Layer-entry travel is adapted to interleave two parts safely instead of executing an unlifted cross-part wipe or printing a full-height channel beside a short one.

Stale source time estimates, duplicate progress/object markers, layer-entry timelapse wrappers, and the uploaded startup/shutdown blocks are not inserted between parts. One final shutdown is used after both complete channels, with final parking Z positions raised by the platform thickness. Physical global layer progress is 1–139.

## Validation

Final replay compares all 11,732 left and 11,749 right channel deposition moves against the originals after translation and the +0.60 mm Z offset. It verifies E, F, acceleration, all fan states, nozzle/bed/K and source scarf heights. The complete platform executable prefix is independently compared byte-for-byte. Checks also cover all 129 layers from each upload, total physical height 8.34 mm, safe initial side transfers, relative extrusion state, one balanced object block and no repeated channel startup/calibration.

All model points remain within the original platform startup's mesh envelope and well inside the plate. The SVG/PNG show the complete top-view projection, a dimensioned bottom-left inlet detail using the stated reference lines, and the layer stack with distinct platform/channel settings. The CSV gives each source layer's settings and scarf Z range. The JSON includes provenance and fitted center/translation values.

Static validation passed; this newly assembled job has not been physically printed.
