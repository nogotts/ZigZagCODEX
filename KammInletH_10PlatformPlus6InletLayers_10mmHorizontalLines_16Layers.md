# KammInletH: seventeen-layer assembly with continuous roofs

The existing filenames are retained. They are legacy names containing `16Layers`; the actual updated print has **17 physical layers**, ending at **Z1.020 mm**. The first sixteen executable printing layers are preserved verbatim. One roof layer is added after the sixth channel layer, before the single final shutdown.

## Roof: one continuous path per side

Each roof starts at its bottom outer horizontal endpoint, extrudes once along the bottom arm, follows the supplied curved/vertical/connecting path continuously upward, then follows the top arm outward to its endpoint. There are no travels, primes, retractions or pauses inside either roof path. The left roof completes before the right roof begins.

The uploaded FullControl files contained overlapping extrusion passes on the horizontal arms. Those duplicate passes are removed. Their geometric union becomes one **10.800 mm horizontal extrusion move** on each bottom and top arm. Each complete side uses **15 deposition moves**, including **two true circular arcs**, instead of the source file's 934 sampled deposition moves. The left curved and connecting features are retained. Per the latest instruction, the right roof is now an exact geometric reflection of the left roof about X128; the differing neck geometry in the uploaded RightRoofLoop file is not used.

Roof endpoints touch the starting points of the inner horizontal lines in the existing channel layers:

| Side | Bottom roof start, mm | Top roof end, mm |
|---|---|---|
| Left | X113.920016, Y116.671949 | X113.920016, Y139.326724 |
| Right | X142.079984, Y116.671949 | X142.079984, Y139.326724 |

Left bottom deposition travels inward to the right and its top arm finishes outward to the left. The right side travels inward to the left at the bottom and outward to the right at the top. Both start at the bottom and finish at the top.

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
