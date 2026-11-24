# Kamm assembly: 10 platform + 8 replacement channel + 1 roof + 122 upper inlet layers

Updated in place. Legacy filenames are retained, including the `6InletLayers`, `16Layers` and `All139Layers` text. The actual print now contains **141 layers**, each nominally 0.06 mm, and ends at **Z8.460 mm**.

| Global layers | Nominal Z (mm) | Printed paths and speeds |
|---|---|---|
| 1–10 | 0.06–0.60 | Original platform/scaffold and lead-ins; executable code unchanged |
| 11–18 | 0.66–1.08 | All eight layers from each new left/right channel file; first channel layer 3 mm/s, next seven 5 mm/s |
| 19 | 1.14 | Existing roof loops, circular finishes and full-roof fills; original 4 and 2 mm/s settings retained |
| 20–141 | 1.20–8.46 | Existing 122-layer upper inlet continuation; first inlet layer 3 mm/s, remaining layers 4 mm/s |

## Channel geometry and alignment

`LEFTinletKamm8.gcode` replaces the left channel and `RIGHTinletKamm8.gcode` replaces the right channel. Each complete eight-layer model is rigidly translated in XY and receives a +0.600 mm Z offset. No scaling, reflection, path simplification or rotation is applied: each uploaded file already has its corresponding orientation.

The same lower circular-center targets used by the previous assembly define the placement. The uploaded circles are polygonal, and their fitted upper/lower center separations differ slightly from the previous file. Lower fitted centers match their targets before coordinate rounding; upper fitted-center residuals are 0.00467 mm left and 0.00541 mm right. The entire side remains a single rigid translation so none of its shapes are distorted. Full fitted centers, radii, translations, source hashes and residuals are in the validation JSON.

## Per-layer order and retained lead-ins

For each layer 11–18:

1. Complete left channel loop, including its original scarf seam and wipe.
2. Left diagonal lead-in from its established outer endpoint to its established inward endpoint.
3. Complete right channel loop, including its original scarf seam and wipe.
4. Right diagonal lead-in.
5. Left bottom horizontal pair, then left top pair.
6. Right bottom horizontal pair, then right top pair.

The two diagonal roads and eight horizontal roads retain their exact XY coordinates, E amounts, nominal 0.30 mm widths, flow ratio 1.4, 25 mm/s speed, acceleration and cooling states. Layers 17 and 18 repeat the prior layer16 lead-ins at increased Z. The last-layer scaffold cooling PWM158 is explicitly retained while the uploaded channel loops use their own source fan schedule.

There are now **144 horizontal roads** across layers 1–18 and **16 channel-stage diagonal lead-ins**. The separate platform diagonal roads on layers 1–10 remain unchanged.

## Machine and extrusion settings

One original startup and calibration sequence is retained before the platform. No uploaded startup, timelapse, purge, homing or shutdown blocks are inserted into the channel stage. The prior off-part temperature transition remains parked at X20 Y220 Z5; no extra thermal waits were added. Bed remains **70°C**. Channel/roof/upper inlet nozzle remains **245°C**, with K0.05; original platform settings remain unchanged.

New channel deposition retains the uploads’ **3 then 5 mm/s**, variable widths, E values, flow already baked into E, acceleration, fans and scarf Z ramps. Their standalone 85°C bed request is excluded in favor of the established 70°C assembly setting. Both source first-layer retractions are omitted because the preceding paths already finish retracted; source primes and final wipes are retained.

The upper inlet stage keeps its previously requested **3 then 4 mm/s**, independent of the new lower channel files’ speeds.

## Shifted roof and upper stage

Every existing roof/upper-stage XY coordinate, E/F/I/J value, fan/temperature/K/acceleration state and path order is retained. All absolute motion Z values and nominal layer-height comments in that portion are increased by exactly **0.120 mm**, including scarf ramps, travel lifts and height-relative shutdown parks. Global layer progress is increased by two.

The existing roof-to-RoofLoop overlap is unchanged by this revision.

## Validation and diagrams

Independent replay checks all **1,370 uploaded channel deposition moves** against source XYZ/E/F/width/acceleration/fan/K/nozzle settings, all 80 channel-stage lead-in roads against their previous settings, and all **20,666 existing roof/upper deposition moves** against their prior settings with the required Z offset. The first ten executable layers are byte-identical. No movement segments were added to the uploaded geometry.

The SVG/PNG top-view schematic shows the new channel paths. The self-contained `KammInletH_All139Layers_3D.html` viewer now displays **141 layers and all 30,576 model extrusion moves**. Download the HTML with GitHub’s **Download raw file**, then open it in a browser to rotate, isolate layers and inspect actual commands. Curves in the 3D view are sampled only for display; that does not segment the print G-code.
