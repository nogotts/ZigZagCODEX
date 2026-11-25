# NOSCARF — complete offline3D preview

All18260 deposited moves are represented, with travel, wipe and prime displays available. Main layers20–141 use the uploaded no-scarf inlet toolpaths. Lower channel scarf seams remain.

# NOSCARF — four upper inlets, separate version

This file retains the existing FIX2.0 executable commands through main layer19, including the ten remote conditioning passes, the lower channels and their5mm scarf seams, and the extended roof finishes. **NOSCARF refers only to the four upper inlet nozzles.** The original FIX2.0 files are untouched.

All122 print layers from `4inletKammNoSCARF.gcode` replace the upper-inlet continuation. Source layer1 starts immediately above the roof as main layer20 atZ1.200mm. Source layer122 becomes main layer141 atZ8.460mm. The source first layer runs2mm/s and later layers4mm/s. All8278 source deposition moves retain their E values, F values, actual Arachne widths, geometry, cooling and acceleration. Source-native inter-ring travel, retractions, unretractions and wipes are retained. Original layer-entry travel is replaced by a raised entry appropriate to the assembly; the first entry uses the outside corridor.

Per user selection, extrusion is preserved exactly as uploaded: the source profile requests a0.30mm first layer and0.21mm outer wall, but Arachne actually generates widths roughly0.213–0.228mm. These actual widths/E values are used, rather than forcing the previous version's0.30/0.21mm roads. No rescaling of E or double flow multiplier is applied. Flow0.98 is baked into source E. Existing nozzle245°C, bed70°C andK0.05 are retained; no source startup, purge, homing, calibration or heater wait is inserted.

Each ring receives its own rigid XY translation to match the existing ring centre. There is no scaling or rotation. All source Z coordinates are shifted+1.140mm. All upper deposition moves are flat within their layer, confirming there are no upper scarf ramps. The existing final shutdown is retained once.

Validation checks all8278 source deposition moves and13924 body commands, native trailing wipes/fan commands, XY registration, Z offsets, E/F/widths, and unchanged first19-layer executable prefix. The new version contains18260 deposition moves; the original FIX2.0 version remains available separately. The drawings show nozzle centrelines, not measured plastic. Passing G-code checks does not establish a physical seal.
