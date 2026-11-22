# KammInletH: seventeen-layer assembly with continuous roofs

The existing filenames are retained. They are legacy names containing `16Layers`; the actual updated print has **17 physical layers**, ending at **Z1.020 mm**. The first sixteen executable printing layers are preserved verbatim. One roof layer is added after the sixth channel layer, before the single final shutdown. That same layer 17 contains the two original continuous roof paths, then four mirrored `HalfCircleFinish.gcode` paths, then two full-roof overhang fill paths. No eighteenth layer is added.

## Roof: one continuous path per side

Each roof starts at its bottom outer horizontal endpoint, extrudes once along the bottom arm, follows the supplied curved/vertical/connecting path continuously upward, then follows the top arm outward to its endpoint. There are no travels, primes, retractions or pauses inside either roof path. The left roof completes before the right roof begins.

The uploaded FullControl files contained overlapping extrusion passes on the horizontal arms. Those duplicate passes are removed. Their geometric union becomes one **10.800 mm horizontal extrusion move** on each bottom and top arm. Each complete side uses **15 deposition moves**, including **two true circular arcs**, instead of the source file's 934 sampled deposition moves. The left curved and connecting features are retained. Per the latest instruction, the right roof is now an exact geometric reflection of the left roof about X128; the differing neck geometry in the uploaded RightRoofLoop file is not used.

Roof endpoints touch the starting points of the inner horizontal lines in the existing channel layers:

| Side | Bottom roof start, mm | Top roof end, mm |
|---|---|---|
| Left | X113.920016, Y116.671949 | X113.920016, Y139.326724 |
| Right | X142.079984, Y116.671949 | X142.079984, Y139.326724 |

Left bottom deposition travels inward to the right and its top arm finishes outward to the left. The right side travels inward to the left at the bottom and outward to the right at the top. Both start at the bottom and finish at the top.

## Four circle finishes after both roofs, on the same layer 17

The uploaded `HalfCircleFinish.gcode` is scaled uniformly by **0.655871974085844**, using its long horizontal source run of 16.477789 units as the **10.807320 mm** scale reference. The complete uploaded model geometry is retained, excluding its standalone startup, primer and shutdown. The resulting curve radius is approximately 1.539998 mm. Its full circular sweep is 264.410204°, as in the source; the filename does not mean the source contains only a 180° arc.

Print order after both existing roof paths: **left top → left bottom → right top → right bottom**. Every finish remains at **Z1.020 mm on layer 17**. Each is one 10.80732 mm horizontal deposition move followed immediately by one true circular arc, with no travel or retraction between them. The source path's curve fit residual is below 0.000001 mm after scaling; the actual fitted-arc path deviates from the original uploaded chordal path by at most 0.000087 mm.

| Copy | Starting endpoint, mm | Mirror reference |
|---|---|---|
| Left top | X113.920016, Y139.476724 | Original aligned source |
| Left bottom | X113.920016, Y116.521949 | Left top reflected about Y127.9993365 |
| Right top | X142.079984, Y139.476724 | Left top reflected about X128 |
| Right bottom | X142.079984, Y116.521949 | Both reflections |

These are the original outer starting endpoints of the **topmost and bottommost horizontal lines**, the outward member of each 0.15 mm-spaced pair. They differ from the inner-pair anchors used by the preceding 10.8 mm roof paths. The source offsets naturally place the new circular curves on the same inlet centers.

The finish paths inherit the layer 17 settings: nominal width 0.30 mm, layer height 0.06 mm, flow 1.4 baked into E once, 4 mm/s, 2000 mm/s² acceleration, 245°C nozzle, 70°C bed, K0.05 and unchanged part-fan PWM158. E is recomputed for each full line and actual G2/G3 arc length. Only the mathematical model path is taken from the new FullControl file; none of its generic homing, heating, purge or shutdown commands is copied.

Each finish is approached retracted at Z1.42, lowered to Z1.02, and primed 0.4 mm before its uninterrupted extrusion. At the end, the 0.4 mm retraction follows the just-printed arc backward for 2 mm, rather than wiping across an unprinted shortcut. It then lifts to Z1.42 for the next mirrored copy. There are no additional thermal waits, fan/K changes or layer changes.

The previous complete executable prefix, including both roof paths, is unchanged. The original single final shutdown is also unchanged. The SVG/PNG overlays all four new paths on the assembly and adds a separate magenta finish panel, with green starts and red ends. All displayed curves are calculated from the actual arc centers and directions.

Independent checks verify all four anchor coordinates, X/Y mirror geometry and E values, 10.80732 mm horizontal lengths, the full original arc sweep, width/flow/E/speed/temperature/fan/K state, balanced primes/retractions, reverse arc wipes, mesh coverage, unchanged preceding code and shutdown, and exactly 17 physical layers. There are only 8 new positive-XY deposition moves total.

## Full-roof overhang fills on layer 17

After both roof outlines and all four circular finishes complete, the new left full-roof fill prints, followed by its exact right-side reflection. All eight layer 17 components start at their outer endpoints and initially extrude inward: left components move left-to-right, right components move right-to-left. The existing continuous paths and their earlier deposition directions/settings are retained; no existing path is redrawn or double-printed.

The longest straight diagonal in the uploaded `LeftFullRoof.gcode` is 14.942085922 source units. The uniform scale **0.831810904108054** makes that diagonal **12.428990 mm**. Its outer endpoint is registered to the existing outer left diagonal endpoint **X113.616990/Y123.172541**. The right fill starts at its exact reflection **X142.383010/Y123.172541** about X128. This positions the first fill track at approximately X125.950002 on the left and X130.049998 on the right, at the existing outer channel walls.

The provided right file describes the same mirrored pattern in reverse order. It is reversed to start at its outer diagonal endpoint, and the emitted geometry uses an exact reflection of the left. The supplied reversed-right geometry differs from that exact mirror by less than 0.000002 mm due to source coordinate rounding.

Each drawn pattern contains the long diagonal, eight long parallel passes and seven short connecting segments. The full path is extruded continuously in 16 straight deposition moves per side, reduced from 2848 sampled moves in each upload. All source model vertices lie within 0.000002 mm of the emitted path. Short connectors remain extruded because they are part of the user's drawn continuous path; no arbitrary travel gaps or stops are introduced between bands.

The adjacent path-centerline spacing is nominally **0.150 mm** (actual rounded coordinates 0.149990–0.150009 mm). With **0.300 mm nominal width**, this is **0.150 mm nominal overlap**. The supplied geometry is retained rather than generating a different fill pattern. Actual material width/overlap still depends on deposition and the retained flow ratio.

### Orca reference motion and cooling

The working `cantilver_PETG_9m25s.gcode` and `LongOVERHANG2_PETG_16m19s.gcode` wave-overhang sections use 2 mm/s deposition (F120), part fan 100% (PWM255) and acceleration 2500 mm/s². Those settings are applied to the **two new full-roof fills**, with 40 mm/s retracted transfer speed. The earlier layer 17 outline and finish paths retain their existing 4 mm/s settings and inherited PWM158 fan state. Fan 255 is enabled before the new fill approaches, held across both fills, and the former fan/acceleration/feed state is restored before the unchanged original shutdown. No cooling/heating dwell is added.

The new fill E values are calculated for the requested nominal width 0.30 mm, the existing layer height 0.06 mm, 1.75 mm filament and retained flow 1.4, rather than copying absolute extrusion from 0.4 mm-nozzle/0.2 mm-layer references. The geometry-derived bead area and actual segment length determine E. Temperatures remain 245°C nozzle/70°C bed, K remains 0.05, and M221 remains 100%. The references' unrelated startup, bed/nozzle profile, homing and calibration are not inserted.

Each side is approached retracted at Z1.42, lowered to Z1.02, primed 0.4 mm, and extruded continuously. It ends with a 0.4 mm retraction during a 2 mm backward wipe on the final vertical fill pass, then lifts again. No added layer change occurs. All old executable commands before the new fills and the entire old final shutdown are unchanged.

Independent replay verifies the scaled 12.42899 mm diagonal, exact anchors and mirror symmetry, nominal 0.15 mm pitch/overlap, sixteen uninterrupted moves per side, source shape preservation, actual E, 2 mm/s speed, fan 255, acceleration 2500, temperatures/K, balanced retract/prime amounts, mesh coverage and unchanged seventeen-layer count. Every prior layer 17 component's first deposition direction is checked against its outside-to-inside requirement. The SVG/PNG overlays the full fills in green and adds a dedicated full-roof panel.

## Correct scale and circle dimensions

The complete horizontal span formed by overlapping source passes is **7.566055 source units**. Scaling that span by **1.427428164347206** gives **10.800 mm**. Measuring an individual source pass instead would give the wrong scale. The radius of each fitted roof curve at the corrected scale is **1.540000 mm** within export/fit tolerance; the existing channel circular regions retain their **1.645 mm nominal outer radius** (3.29 mm diameter).

The uniformly scaled roof source has nominal lower-to-upper center spacing **22.656152671 mm**, consistent with the user's 22.65612 mm CAD dimension within approximately 0.000033 mm export rounding. The existing horizontal anchor lines in the assembly are **22.654775 mm** apart. To touch both existing starts exactly without changing any old layer or distorting the curves, only the long straight roof connector is shortened by **0.001377671 mm**. The entire upper roof region is translated by that amount; its curves, angles and horizontal arm lengths are preserved. There is no anisotropic scaling of either circular region.

Quarter-circle fits have radial residuals below 0.000005 mm. Collinear cleanup is bounded by 0.000003 mm, and the fitted arc-to-original-chord deviation is below 0.0005 mm. The two 10.8 mm arms on each side are each represented by one deposition move.

## Roof extrusion and motion settings

The roof inherits the existing assembly's extrusion and motion settings except for the requested 4 mm/s deposition speed and explicit nominal width 0.30 mm:

| Setting | Roof value |
|---|---|
| Printed layer | 17, at Z1.020 mm |
| Layer height | 0.060 mm |
| Nominal width | 0.300 mm |
| Flow ratio | 1.4, included in E once |
| Filament diameter | 1.75 mm |
| Deposition speed | 4 mm/s (F240) |
| Deposition acceleration | 2000 mm/s² |
| Nozzle / bed | 245°C / 70°C |
| Pressure advance | K0.05 |
| Part fan | Existing final-channel PWM158, about 62%; unchanged |
| Auxiliary / chamber fan | Existing PWM0 / PWM255; unchanged |

E is recalculated using actual line/arc length, rounded-rectangle bead area `(width−height)×height + π×(height/2)²`, the filament area and flow 1.4. M221 remains 100%. Arc E uses the replayed I/J radius and sweep. Nominal width and calculated volume are not measurements of physical printed width.

Each side is approached while retracted at Z1.420, then lowered to Z1.020 and primed by 0.4 mm. Transfers use the outside and above-part corridors where practical. After the complete continuous path, a 0.4 mm retraction occurs during a 2 mm backward wipe along the final horizontal arm, followed by a lift. No extra source startup, calibration, purge, homing, heating wait, fan changes or source shutdown is inserted.

The original single shutdown is retained with its height-dependent parks raised by 0.06 mm: Z1.52, Z101.02 and Z99.02. Its machine parking coordinates and heater/fan shutdown commands remain unchanged.

## Existing sixteen-layer assembly retained

Layers 1–10 retain both original scaffolds, eight horizontal lines per layer and both earlier angled strokes. Layers 11–16 retain the uploaded six-layer channel contours, each followed by its diagonal intro, then the eight extended horizontal roads. Those roads keep their fixed outer starts and 0.300 mm endpoint clearance from the nominal 3.29 mm circular-region outer circumferences. Widths, E values, F values, acceleration, scarf ramps, fans, heaters, K and geometry of all sixteen layers are unchanged.

The original startup, purge and adaptive leveling region are retained. The base remains 255°C nozzle/70°C bed/K0.55, the channel stage 245°C/70°C/K0.05, and its nozzle-temperature wait remains parked off the print at X20/Y220/Z5. The roof repeats no startup or calibration. The original channel source flow 0.98 and added-line flow 1.4 remain included in their respective E values once.

## Diagram and checks

The same SVG/PNG overlays the new roof on the complete assembly and adds a large roof-only panel with bottom START and top END markers, direction arrows and both 10.800 mm arm dimensions. Roof previews are now generated directly from the actual G-code G1/G2/G3 motions and I/J arc centers. This corrects the previous SVG arc-sweep rendering error; the left roof G-code itself is unchanged. Right-roof X coordinates are reflected about X128, Y/E values are identical to the left, I offsets are negated, J offsets are unchanged, and G2/G3 handedness is reversed. Existing circle-clearance detail panels still describe layers 11–16, not the added roof.

Independent replay verifies the complete sixteen-layer executable prefix is unchanged, there are exactly 17 layer-change records, and every one of the 30 new roof deposition moves has the expected XYZ, speed, width, E, acceleration, K, temperatures and inherited fans. Checks verify continuous paths, exact anchor endpoints, single 10.8 mm arms without duplicated passes, 1.54 mm arc radii, balanced primes/retractions, mesh coverage, one object scope and shutdown, and the rebased final parking heights. A separate comparison verifies the right roof is an exact mirror of the left and that the corrected preview traces come from the final G-code. The actual left arc trace matches the original uploaded left geometry within 0.000412 mm (the original chord-to-circle sagitta).

These are static geometry/G-code checks. The roof has not been physically printed.
