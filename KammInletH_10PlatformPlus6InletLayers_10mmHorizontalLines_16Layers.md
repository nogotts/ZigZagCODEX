# Kamm assembly: 10 platform + 8 replacement channel + 1 roof + 122 upper inlet layers

Updated in place. Legacy filenames are retained, including the `6InletLayers`, `16Layers` and `All139Layers` text. The actual print now contains **141 layers**, each nominally 0.06 mm, and ends at **Z8.460 mm**.

| Global layers | Nominal Z (mm) | Printed paths and speeds |
|---|---|---|
| 1–10 | 0.06–0.60 | Original platform/scaffold and lead-in deposition retained; travel revised |
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

The two diagonal roads and eight horizontal roads retain their exact XY coordinates, E amounts, nominal 0.30 mm widths, flow ratio 1.4, 25 mm/s speed, printing acceleration and cooling states. Their explicit pressure advance is now K0.55, matching the earlier lead-ins; source channel K0.05 is restored after each lead-in group. Layers 17 and 18 repeat the prior layer16 lead-ins at increased Z. The last-layer scaffold cooling PWM158 is explicitly retained while the uploaded channel loops use their own source fan schedule.

There are now **144 horizontal roads** across layers 1–18 and **16 channel-stage diagonal lead-ins**. The separate platform diagonal roads on layers 1–10 remain unchanged.

## Machine and extrusion settings

One original startup and calibration sequence is retained before the platform. No uploaded startup, timelapse, purge, homing or shutdown blocks are inserted into the channel stage. The prior off-part temperature transition remains parked at X20 Y220 Z5; no extra thermal waits were added. Bed remains **70°C**. Channel/roof/upper inlet nozzle remains **245°C**, with K0.05; original platform settings remain unchanged.

New channel deposition retains the uploads’ **3 then 5 mm/s**, variable widths, E values, flow already baked into E, acceleration, fans and scarf Z ramps. Their standalone 85°C bed request is excluded in favor of the established 70°C assembly setting. Both source first-layer retractions are omitted because the preceding paths already finish retracted; source primes and final wipes are retained.

The upper inlet stage keeps its previously requested **3 then 4 mm/s**, independent of the new lower channel files’ speeds.

## Shifted roof and upper stage

Every existing roof/upper-stage XY coordinate, E/F/I/J value, fan/temperature/K/acceleration state and path order is retained. All absolute motion Z values and nominal layer-height comments in that portion are increased by exactly **0.120 mm**, including scarf ramps, travel lifts and height-relative shutdown parks. Global layer progress is increased by two.

The existing roof-to-RoofLoop overlap is unchanged by this revision.

## Validation and diagrams

Independent replay checks all **1,370 uploaded channel deposition moves** against source XYZ/E/F/width/acceleration/fan/K/nozzle settings, all 80 channel-stage lead-in roads against their previous settings, and all **20,666 existing roof/upper deposition moves** against their prior settings with the required Z offset. The first ten layers retain their original deposition geometry and extrusion; travel has been revised as described below. No movement segments were added to the uploaded geometry.

The SVG/PNG top-view schematic shows the new channel paths. The self-contained `KammInletH_All139Layers_3D.html` viewer now displays **141 layers and all 30,576 model extrusion moves**. Download the HTML with GitHub’s **Download raw file**, then open it in a browser to rotate, isolate layers and inspect actual commands. Curves in the 3D view are sampled only for display; that does not segment the print G-code.

## Slower lead-in transfers and original wipe behavior

All **180 horizontal/diagonal lead-in roads** retain their original extrusion start/end coordinates, E values, nominal widths and printing speeds. In particular, the diagonals on layers 11–18 start at **left X113.616990 Y123.172541** and **right X142.383010 Y123.172541**, exactly matching the earlier diagonal outer starts.

The old lead-ins inherited K0.05 after layer10. They now explicitly use **K0.55**, consistent with the earlier lead-in lines; each group restores the source profile's K value before channel/roof deposition. This makes the commanded settings consistent but does not guarantee physical width or immediate flow without a print check.

The exact existing **2 mm wipe with E−0.4 at F600** is retained after each lead-in. **No new shake, oscillation, or unsupported Bambu command has been added.** After wiping, the nozzle lifts to **1 mm above the current nominal layer**, returns outward along its own road while retracted, and parks outside the complete model footprint.

Transfers use exterior corridors at **X112.616990 / X143.383010** and **Y113.710299 / Y142.289701**. XY travel is capped at **40 mm/s**; short approaches, raised own-road returns and structure entry/exit use **20 mm/s**; Z moves use **10 mm/s**. Route acceleration is **1000 mm/s²** and each printing move restores its original printing acceleration.

Channel/platform entry is approached through the center gap at X128 at the raised clearance, followed by a short final approach over its own structure. It is impossible to enter or leave an interior endpoint without passing above some of its footprint; this revision limits that to short raised entry/exit moves and raised returns along the road itself. Long transfers use the exterior and center corridors. The final intro line no longer parks over the print before the next layer.

The first approach to the roof is also slowed to 40 mm/s. All subsequent roof and upper inlet code is unchanged. The roof overlap remains unchanged.

## Separate 18-layer diagnostic

`18layer_KammInletH_10PlatformPlus8ChannelLayers_SlowTravel.gcode` contains the **identical updated full-file prefix through completed layer18**, preceded only by three identifying comments. It then parks outside the print and uses the normal shutdown with height-dependent Z parks rebased to **1.08 mm**. It prints no roof or upper inlet continuation. The diagnostic SVG/PNG shows the lead-in and raised travel routes; its validation JSON records the shared prefix hash. Startup/calibration is included once, exactly as in the full file.
