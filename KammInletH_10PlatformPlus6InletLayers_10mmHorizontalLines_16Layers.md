# KammInletH: ten platform layers plus six replacement inlet layers

This replaces and renames the previous `KammHorizontal_10mmInletLines_0p5mmGap_10PlatformPlus129ChannelLayers` artifact set. The new G-code, SVG, PNG and validation report use the prefix `KammInletH` and describe the shortened 16-layer assembly. Historical assembly variants elsewhere in the repository are unchanged.

## Printed sequence

Layers 1–10 are copied verbatim from the uploaded KammHorizontal G-code, including startup, purge, expanded leveling area, original platform paths, and all forty 10 mm horizontal roads. Their order remains left structure → lower left road → upper left road → right structure → lower right road → upper right road at each height.

Layers 11–16 now contain only layers 1–6 from `KammInletChannel1_Left.gcode` and `ChannelRightNEw.gcode`. The left and right sources are interleaved at each height. Their Z coordinates are shifted upward by exactly 0.600 mm to sit on the unchanged platform. Source scarf Z ramps are retained. The inlet stage has six 0.06 mm layers, from nominal Z0.66 through Z0.96 mm, giving 16 physical layers and a 0.960 mm final printed height. No source layer 7 or later, roof, or wave-overhang replacement is printed.

## Alignment

The source files are used in their original left/right orientations. Only rigid XY translations are applied; there is no scaling, rotation, or newly synthesized mirror path. Exposed first-layer lower inlet ring vertices are fitted to determine each source center, then aligned to the corresponding ring center in the uploaded existing assembly.

- Left lower inlet center: X126.260016, Y116.671949 mm.
- Right lower inlet center: X129.739984, Y116.671949 mm.
- Left source translation: X−1.742390250, Y+2.000132653 mm.
- Right source translation: X+1.737483390, Y+2.000120214 mm.

The upper-circle fitted centers match the old corresponding upper-circle fits within 0.000100 mm on the left and 0.000034 mm on the right. These small differences are below the source polygon/coordinate rounding uncertainty; no deformation of the supplied paths is introduced to eliminate them. Circle fit maximum radial residuals are below 0.003 mm. Detailed fitted centers and residuals are recorded in the validation JSON.

The SVG retains the full platform and horizontal-road schematic. Magenta paths show the replacement inlet contours at global layer 16; dashed circles show the inlet alignment with the specified 3.29 mm outer diameter. The horizontal roads and their 0.500 mm centerline gaps remain unchanged.

## Settings and motion

The platform settings remain unchanged: 255°C nozzle, 70°C bed, K0.55, nominal width 0.15 mm, flow 1.4 baked into E, first layer 5 mm/s and later platform layers 25 mm/s, with the original fan schedule.

The six inlet layers retain the newly supplied slicer files' E values, F values, variable widths, acceleration, scarf ramps, and fan commands. Inlets use 245°C nozzle, K0.05, and source flow 0.98 already included in E. Source inlet layer 1 prints at 3 mm/s and source layers 2–6 at 5 mm/s. The bed remains 70°C, preserving the existing assembly's deliberate override of the source files’ 85°C bed profile. New source startups, calibration, purges, shutdowns, object scopes and obsolete layer/time metadata are not repeated.

The existing stage transition is retained: retract state comes from the platform wipe, lift to Z5, move to X20/Y220, complete the parking move with M400, and wait for 245°C there. There is no bed-temperature wait between stages. Each source component is approached while retracted at 0.40 mm above its nominal layer and restores its own feedrate, acceleration, and fan states before printing. Its original prime and final wipe are retained, including the source's trailing wipe that appears after the next CHANGE_LAYER comment in standalone files.

One final normal shutdown follows the right inlet's sixth layer. Height-dependent parking positions are rebased to the shortened part: initial shutdown lift Z1.46, final bed presentation Z100.96 then Z98.96. There is one startup, one object scope, and one shutdown.

## Validation

Static checks passed: the entire executable startup/platform prefix is byte-for-byte identical to the uploaded KammHorizontal source; all 40 horizontal roads are retained; there are exactly 16 physical layers and six source layers per side. Independent checks compare all twelve source body/wipe sections: all E/F/I/J tokens are unchanged and all XYZ tokens differ only by the documented rigid translations. All994 channel deposition moves retain their source extrusion, speed, width, acceleration and fans, and their Z ramps receive only the 0.60 mm offset. Retraction/prime balances are preserved, the only post-platform thermal wait occurs at the off-part park, and no roof/overhang stage remains. Final printed Z is 0.96 mm.

These are G-code and alignment checks; the shortened assembly has not been physically printed.
