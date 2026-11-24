# FIX — approved mirrored assembly; corrected post-layer10 lead-in K and flow

All25related deliverables are renamed with `FIX_`. The remaining legacy `6InletLayers`, `16Layers`, `All139Layers` and `PREVIEW` basename text is retained for continuity; the approved full file actually contains **141layers / Z8.460mm**.

| Portion | Layers | Speed | K | Flow ratio |
|---|---|---|---|---|
| Platform / early lead-ins |1–10|Original5then25mm/s|0.55|1.4|
| Approved channel walls |11–18|3then5mm/s|0.05|Original source0.98 baked into E|
| All horizontal and diagonal lead-ins |11–18|**25mm/s, unchanged**|**0.05**|**0.98 baked into E once**|
| Existing roof paths |19|Original4and2mm/s|0.05|Original1.4 retained|
| Upper inlet walls |20–141|Original3then4mm/s|0.05|Original source extrusion retained|

## Approved geometry and scarf profiles

All eight channel layers start upward at **Y123.500**, at X125.943398left / X130.056602right. Left is clockwise, right counterclockwise, exact reflections aboutX128. The first source layer remains flat; all original1.5mm scarf E/Z profiles on source layers2–8 remain exactly as approved. No further scarf tuning is applied.

The first ten layers' deposition geometry and E values remain unchanged. The roof and upper inlet deposition geometry, E and printing settings remain unchanged. Final roof layer19 is at Z1.140; upper inlets begin layer20/Z1.200.

## Latest K and flow request

All **80lead-in roads on layers11–18** (64horizontal +16diagonal) now use **K0.05 / flow0.98**, matching the channel's settings. All deposition after layer10 usesK0.05. Only the post-layer10 lead-in E values are reduced by **0.98/1.4 =0.7**, with nominal width0.30mm and endpoints unchanged. `M221` stays100; no second flow multiplier is applied.

The additional diagonal slow-start proposal has been **removed**. Each diagonal is once again its original single deposition move at25mm/s, with the normal0.4mm unretraction at the original speed. No extra priming, dwell, movement segmentation or experimental pressure tuning is added. Lead-ins on layers1–10 retainK0.55/flow1.4.

## Endpoint and travel behavior

The188custom backward wipes on lead-ins and custom roof components are removed. Those paths stop at their extrusion endpoints and retract0.4mm **without XY motion**, then lift before traveling. The original slicer-authored wipes on the uploaded closed platform/channel/upper-inlet loops remain unchanged. No custom shake/jolt is added.

Raised travel retains the outside/center corridors and1mm nominal clearance for lead-ins and roof handoffs. Maximum exterior travel40mm/s, short raised approach/return20mm/s, Z10mm/s. A raised return toward an exterior lane is travel in the air, not wiping backward on the deposited line.

## Files and verification

- `FIX_KammInletH_10PlatformPlus6InletLayers_10mmHorizontalLines_16Layers.gcode`:141layers,30,599deposition moves, finalZ8.460.
- `FIX_18layer_KammInletH_10PlatformPlus8ChannelLayers_SlowTravel.gcode`:the exact full printing prefix through layer18, then parked shutdown;9,933deposition moves, finalZ1.080. No roof or upper inlets.
- `FIX_PREVIEW_Y123p5_MirroredChannels_LeftCW_18Layers.gcode`:renamed approved-preview diagnostic copy of the same18-layer print.
- `FIX_KammInletH_All139Layers_3D.html`:offline rotatable viewer. Download raw HTML and open locally; hover shows E, speed, width, fan and K.

All checks passed for approved mirror/winding and scarf profiles, unchanged non-target deposition, all180lead-in endpoints, all80post-layer10 E reductions, K0.05 on all printing after layer10, unchanged lead-in printing speeds, and the188stationary endpoint retractions. One startup and one shutdown remain; no new thermal waits were added. Bed70°C and channel/roof/inlet nozzle245°C are retained. Existing roof overlap is unchanged.

## Conditioning line after layer10

After the tenth scaffold layer and the existing245°C/K0.05 transition, a single40mm conditioning line prints from **X90,Y95 to X130,Y95 at build-plate Z0.060mm**. It uses nominal width0.212876mm, flow0.98 baked into E, speed3mm/s, K0.05 and part fan off, matching the first channel road. The line usesE0.19556949mm of1.75mm filament.

XY transfers to and from the remote line occur at **Z5mm** via the outside corridors. It finishes with a stationary0.4mm retraction and no reverse wipe. The original parked entry state atX20,Y220,Z5 is restored before the unchanged layer11 path. The closest model Y is114.710299, leaving **19.710299mm** clear of the line.

The existing startup mesh rectangle is expanded toX89..144.154984,Y94..143.439701 to cover this added build-plate road. No new probing/calibration sequence, thermal wait or layer marker is added. All prior model commands and scarf profiles remain unchanged; the full/test files still print141/18nominal layers. In the3D viewer, the conditioning line belongs to the completed-layer10 processing interval but its actual Z remains0.060mm.
