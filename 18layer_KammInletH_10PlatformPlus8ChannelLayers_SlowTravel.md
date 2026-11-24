# 18-layer Kamm diagnostic — slower outside travel

Prints the same updated platform, channel and lead-in sequence as the full assembly through **layer18 / Z1.080 mm**, then parks outside the print and performs the normal shutdown. No roof or upper inlets are printed.

The first three lines identify this diagnostic; the following full-file prefix is byte-identical through completed layer18. Original startup/calibration is included once. Shutdown height-dependent parks are rebased to this test's actual height.

All 9,910 deposition moves match the first eighteen layers of the updated full file. The new channel walls run at 3 then 5 mm/s; lead-in printing speeds remain unchanged. Added lead-ins use K0.55; channel K0.05 is restored. No extra priming, new shake or oscillation is added: the original 2 mm wipe/E−0.4 is retained.

Raised travel: 1 mm nominal clearance, 40 mm/s exterior maximum, 20 mm/s short approaches/returns, 10 mm/s Z. Long transfers follow exterior corridors. Only short raised structure entry/exit and own-road returns pass above printed paths. The SVG/PNG is a schematic of layer18 deposition and travel; the full 3D viewer can isolate layers1–18.
