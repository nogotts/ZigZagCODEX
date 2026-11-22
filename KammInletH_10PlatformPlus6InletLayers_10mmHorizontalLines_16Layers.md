# KammInletH: 139-layer assembly with aligned four-inlet continuation

Existing filenames are retained. The legacy filename contains `16Layers`, but the actual current print has **139 physical layers** and a final printed height of **8.340 mm**. All printing commands for the previous first seventeen layers are preserved verbatim. The uploaded `4InletKamm0.3First_PETG_44m1s.gcode` is appended immediately afterwards, with its original 122 print layers becoming global **layers 18–139**.

## Print stages

| Global layers | Nominal Z range, mm | Printed geometry |
|---|---:|---|
| 1–10 | 0.06–0.60 | Original mirrored scaffold, horizontal pairs and diagonal leads |
| 11–16 | 0.66–0.96 | Six source channel layers per side, diagonal intros and extended horizontal pairs |
| 17 | 1.02 | Two continuous roof outlines, four circular finishes, then both full-roof overhang fills |
| 18–139 | 1.08–8.34 | All 122 layers of the four-inlet source print, with circular centers registered above layer 17 |

The continuation's first layer prints at **Z1.080 mm**, exactly one 0.060 mm layer above the completed roof. Every source Z coordinate, including scarf ramps and source travel heights, receives a **+1.020 mm offset**. Source maximum deposition height 7.320 mm therefore becomes 8.340 mm. No scaling or layer-height conversion is applied.

## No repeated startup, calibration or warm-up

The original full file still has its one initial P1S startup before layer 1. Between layer 17 and layer 18, the new stage only restores coordinate modes and the source's print feedrate, acceleration, fans and width state. It then begins the first ring immediately after a safe lifted approach.

No appended homing, mesh probing, vibration or flow calibration, purge, temperature-setting/wait sequence, or source startup is inserted. In particular, there are **no M109/M190 waits or new heater setpoints** during the continuation. The source's standalone 85°C bed request is not copied; the existing **245°C nozzle / 70°C bed / K0.05** state is retained. The uploaded first-layer retract is not duplicated: the prior roof's final wipe already leaves the extruder retracted, and the source's original first prime is kept.

All 122 source body sections, their internal travel/retract/prime commands and their final wipes are retained. Metadata/object wrappers and obsolete layer/time progress messages are replaced by the combined file's global 18–139 numbering. There is one object scope and one normal final shutdown after layer 139.

## Circular-center registration

Four disconnected circular regions are each rigidly translated to the matching actual layer 17 finish-circle center. Source ring centers are fitted to the dominant first-layer polygon vertices; intermediate seam points on polygon chords are excluded from the center fit only. **No printed vertex, perimeter, scarf segment or E value is removed or reshaped.** The fit uses 20–21 of 22 unique vertices per ring; maximum inlier radial residual is below 0.0013 mm. This estimates the circle centers from the supplied G-code rather than an unavailable CAD model.

| Region | Target center X, Y, mm | Source XY translation, mm |
|---|---|---|
| left_bottom | 126.260012, 116.671945 | -0.000389537, +2.000464208 |
| left_top | 126.260012, 139.326728 | -0.000466591, +1.999012072 |
| right_bottom | 129.739988, 116.671945 | -0.000414639, +2.000319740 |
| right_top | 129.739988, 139.326728 | -0.000490591, +1.999012072 |

The translations are held constant across all 122 source layers. The circles retain the source geometry and dimensions. Each fitted center coincides with its target before coordinate rounding; after six-decimal output rounding, registration differs by less than 0.000001 mm. The separate translations absorb the source polygon/rounding differences while matching the four existing roof centers.

## Source settings preserved

All **20,596 positive-XY source deposition moves** retain their original E, F, variable width, acceleration, fan state and relative scarf Z behavior. Filament flow 0.98 is already included in the source E values; it is not multiplied again by the earlier custom-line flow 1.4. M221 remains 100%.

The uploaded stage uses a 0.2 mm nozzle and 0.06 mm layers. Its first layer runs at 3 mm/s and its later layers at 5 mm/s, with source acceleration 500 mm/s² on the first layer and 2000 mm/s² on deposition afterwards. Its original part-fan schedule is restored: source layers 1–3 fan off, then PWM229 on subsequent source deposition. Auxiliary/chamber fan states and any within-body settings remain source-preserved. Variable widths, including Arachne and scarf segments, are copied without recalculating E.

Safe approach wrappers lift to 0.40 mm above each new nominal layer before entering the source body. The source's original inter-ring travels and Z moves are translated intact. Prime/wipe amounts, including the source's small decimal rounding residuals, are preserved exactly. All new deposition remains inside the existing adaptive leveling rectangle; no startup/leveling change is needed.

## Existing seventeen-layer base retained

The original base, channel geometry, 0.15 mm-spaced horizontal pairs, 0.30 mm nominal added roads, 0.300 mm circle-boundary endpoint clearances, diagonal intros, continuous roof paths, circular finish paths and full-roof fills remain unchanged.

Layer17 still prints both continuous roofs and four circle finishes at 4 mm/s, followed by full-roof fills at 2 mm/s, 100% part cooling and 2500 mm/s² acceleration. Each full fill retains its 12.42899 mm diagonal and 0.15 mm nominal overlap for 0.30 mm nominal width. Every layer 17 component retains its outer-start/inward-first direction. The current first seventeen executable printing layers match the previous version byte-for-byte.

The original initial startup, purge, temperatures, calibrated K values, adaptive mesh and off-part transition wait between the scaffold and channel stage are unchanged. No earlier source settings are transferred into the newly uploaded source's E values.

## Final shutdown and diagram

The uploaded file's normal P1S shutdown is used once after the entire continuation. Its height-relative parking coordinates receive the same 1.02 mm offset: initial shutdown Z8.84, final bed presentation Z108.34 then Z106.34. Heater/fan shutdown and AMS unloading remain in the final footer only.

The updated SVG/PNG retains the existing geometry/path details, overlays the new first-layer inlet contours, and adds a registration table and a schematic height stack for layers 18–139. It explicitly states that the new stage begins at layer 18 without warm-up or calibration. The height stack is schematic; the source prints ring walls, not solid rectangular columns.

## Verification

Independent replay checks all 122 source bodies against the upload: all 20,596 deposition moves have exactly the source E/F/width/acceleration/fan state and the documented XY translations and +1.02 mm Z offset. Every source body/wipe motion token, including primes, retractions and travels, is compared. Checks confirm all four center registrations, unchanged first seventeen printing layers, no appended startup/heating/calibration, source bed 85°C not copied, first new Z1.08, final Z8.34, exactly 139 physical layers, mesh coverage, one balanced object scope and one rebased final shutdown.

These are static alignment/G-code checks; the combined print has not been physically tested.
