# FIX2.0 — uploaded-start mirrored channel timing at 5 mm/s

Times count deposition distance/feed only. First channel layer actually prints at3mm/s; diagram represents later5mm/s layers.

The uploaded `5mmRIGHTinletKamm8.gcode` supplies all eight channel layers. Its original start point, XY geometry, E, variable Arachne widths, 5mm scarf Z/E ramps and native retracting wipes are preserved. Translation aligns it to the existing assembly. The entire left toolpath is an exact reflection about X128 and runs clockwise; right runs counterclockwise. Starts are leftX125.944122 /rightX130.055878, bothY128.130686. No source startup/calibration is embedded.

The source profile requests0.21mm width; actual Arachne widths are0.212876,0.215626,0.222212 and0.222306mm. Matching straight lead-ins use0.212876mm. Channel layer11 runs3mm/s; layers12–18 run5mm/s. All180 separately added horizontal/diagonal lead-ins were recalculated from their unchanged length, layer height and matched structural width:0.15mm on main layers1–10 and0.212876mm on11–18. Their speeds match the structure:5 then25mm/s for1–10,3 then5mm/s for11–18. Source-native variations around circles remain intact.

After main layer10, K0.05 and flow0.98 apply, with the explicit exception that the complete roof layer19 is unchanged atflow1.4. All roof lead-ins also stayflow1.4 and match their corresponding roof paths:4mm/s for outlines/circular paths,2mm/s for fill. Every roof executable command is identical to the previous revision. Flow is baked into E once, with M221S100. Upper-inlet continuation already uses the source0.98 profile and its executable commands remain unchanged. Nozzle245°C, bed70°C after10. First-ten structural settings and machine setup are retained.

Before main layer11: ten stacked40mm conditioning lines fromX90,Y95 toX130,Y95, atZ0.06,0.12,...,0.60mm. Passes1–5 run10mm/s;6–10 run5mm/s. Each useswidth0.212876mm, flow0.98, K0.05, E0.19556949mm filament, fanoff. Each prints left-to-right, ends with stationary0.4mm retract, and returns outside the line atZ5mm. These extra ten conditioning layers do not renumber the main part: main channel layers11–18, roof19, upper inlets20–141. No added probing or heating/calibration sequence.

Native channel wipes are retained; no invented shake or reverse lead-in wipe is added. Lead-in endpoints, external travel corridors and structural XY alignment remain unchanged. This is a command-level validation, not a claim of measured printed bead width or passage patency. Legacy filenames are retained even where they contain old layer counts orY123p5.
