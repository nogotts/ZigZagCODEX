# FIX4.0 — complete assembly

This separate full-print version is based on the complete NOSCARF assembly, not the19-layer test. All141 main layers and the ten remote conditioning passes remain. Previous versions are retained.

## Roof layer19 changes

All four HalfCircleFinishes return to their original arc endpoints, removing the former45° extension. Each original arc is followed immediately by one3.000mm vertical extrusion, aligned with the existing narrow-channel centreline: downward at the top inlets and upward at the bottom inlets. Left/right shapes are exact mirrors. Finish settings remain nominal width0.30mm, height0.06mm, flow1.4, speed4mm/s, K0.05. Arc radius/centre and original horizontal lead-ins are retained. There is no retraction between each arc and its new tail.

After BOTH existing floating-roof fills are complete, a continuous closed border prints around each large central roof box, excluding inlet circles and narrow necks. The box corners are derived from the existing outermost floating-roof roads. Each starts at the midpoint of its outer vertical edge: left clockwise, right counterclockwise. Each uses exactly five connected G1 extrusion moves, with no interruption until it returns to its starting point. Travel between loops occurs retracted and1mm above the roof, via exterior corridors. Borders retain the full floating-roof settings:2mm/s, nominal width0.30mm, height0.06mm, flow1.4, K0.05, fan255/255, acceleration2500mm/s². The prior fan state is restored before the upper-inlet stage.

## Upper inlets

Only the first upper-inlet layer, main layer20, is changed to nominal width0.30mm. Its88 positive deposition E values are rescaled using E_new=E_old*(0.30-0.06*(1-pi/4))/(old_width-0.06*(1-pi/4)), preserving flow0.98 and2mm/s. All remaining uploaded inlet layers21–141 are byte-identical to the complete NOSCARF source, including E, width, speed, geometry, retractions, wipes and cooling. No scarf joints are introduced in the upper inlets. Lower channel5mm scarfs are retained.

Nozzle245°C and bed70°C after layer10 are retained. All other executable commands are unchanged. One original startup and one original shutdown remain. Validation confirms finish lengths, mirrored borders, their direction/closure, print settings, E per unit length, source upper-layer identity and141 main-layer markers. Physical seal quality requires printing and inspection.

Left border start/end: X125.950002,Y128.100916; length28.258861mm.

Right border start/end: X130.049998,Y128.100916; length28.258861mm.
