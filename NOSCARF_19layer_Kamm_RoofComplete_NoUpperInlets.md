# NOSCARF_19layer_Kamm_RoofComplete_NoUpperInlets

Separate version of `NOSCARF_FIX2.0_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode` that completes all roof sections and ends before any upper inlet nozzle prints. The complete source file remains unchanged.

The executable prefix through main layer19 is byte-identical to the source:10 scaffold layers, the unchanged ten-pass remote conditioning stack,8 channel layers, and all roof sections. Layer19 includes both RoofLoops, all four extended HalfCircleFinishes and both full roof fills. The final model deposition ends atX128.999992,Y121.499655,Z1.140000. No layers20–141 or upper-inlet approach are included.

The normal Bambu shutdown follows: finish buffered motion, retract, lift, park, turn off heaters/fans, and retain the existing filament-end sequence. Height-relative shutdown parks change by-7.320mm for the shorter part:Z8.96→1.64,108.46→101.14,106.46→99.14mm. Every other shutdown command is retained. This ends the job; it does not pause for a later resume.

Validation:19 main layer markers,10 conditioning passes,9982 deposited moves, all8 roof sections retained, no upper-inlet stage and no positive deposition after the roof. G-code checks do not establish a physical seal.
