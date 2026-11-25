# FIX2.0 — uploaded-start mirrored channel timing at 5 mm/s

Times count deposition distance/feed only. First channel layer actually prints at2mm/s; diagram represents later5mm/s layers.

The four HalfCircleFinish arcs on main layer19 now continue45° beyond their former endpoints, matching the approximate green portion in the drawing. Each adds1.209512mm along the existing1.539998mm radius. Original centres, arc direction, start points and lead-ins are preserved. Each existing G2/G3 command is extended rather than replaced by short line segments. Arc E increases from0.07126207 to0.08339017mm filament, preserving E per millimetre. Left/right and top/bottom extensions are mirrored. Retraction and raised travel occur after the new endpoint. Roof finishes retain nominal width0.30mm /flow1.4 /4mm/s. All other roof deposition commands, including RoofLoop and full fill, remain unchanged.

Main channel layer11 and all its added diagonal/horizontal lead-ins now print2mm/s. Channel layers12–18 remain5mm/s. Uploaded channel XY,E,Z, actual Arachne widths, 5mm scarf, starting point and clockwise-left/counterclockwise-right mirror are unchanged. Both loops still start atY128.130686, withX125.944122 left /X130.055878 right. Channel straight width0.212876mm corresponds to the source0.21mm profile setting; flow0.98 andK0.05 remain.

The first upper-nozzle layer, main layer20 atZ1.200mm, prints2mm/s with nominal width0.30mm. Later nozzle layers21–141 use nominal width0.21mm and retain their existing4mm/s deposition speeds. Positive deposition E values are rescaled once using E_new=E_old*(new_width-0.06*(1-pi/4))/(old_width-0.06*(1-pi/4)), retaining flow0.98 and source scarf flow fractions. All nozzle XY,Z, original motion segments, retractions, primes, source wipes, cooling and acceleration are unchanged. Actual physical bead width requires measurement.

Main layers1–10 retain their prior structural and lead-in commands:0.15mm nominal width, flow1.4,K0.55, first5 then25mm/s. The remote ten-layer40mm conditioning stack is unchanged: X90,Y95→X130,Y95, Z0.06 through0.60, five passes10mm/s then five5mm/s, width0.212876,flow0.98,K0.05. Return travel is outside atZ5mm. Part layer numbering stays1–141; the remote stack is separate.

After main layer10, nozzle245°C /bed70°C /K0.05 remain. Flow0.98 applies to channels, their lead-ins, conditioning and upper nozzles; the roof retains its explicitly requestedflow1.4. No startup, calibration, homing or temperature wait is added. The18-layer diagnostic includes the channel first-layer speed change and ends before roof/nozzle stages. Legacy FIX2.0 filenames remain unchanged.

Validation compared every executable command against the prior FIX2.0 revision: changes are restricted to126 layer11 deposition feed rates, four arc endpoints/E values, and20596 nozzle deposition E values (including88 first-nozzle-layer feed rates). Every other executable command is identical. G-code checks cannot guarantee a printed seal.
