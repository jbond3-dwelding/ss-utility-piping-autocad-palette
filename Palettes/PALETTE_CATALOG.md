# Palette group: SS Utility Piping

Create 10 tabs (9 piping + 1 supports package). After Design Center build, add **Separators** and **Text** labels inside each tab.

Insertion: fitting / valve center or pipe start at origin. Centerline on Y=0. Flow +X.

## Tab 01 Pipe Sch 10S
- SS-PIPE-BW-025..180-10S (plan double-line, 12 in default length)
- SS-PIPE-SL-025..180-10S (single-line centerline for small-scale plans)
Command: `SSPIPE` schedule 10S

## Tab 02 Pipe Sch 40S
- SS-PIPE-BW-025..180-40S
- SS-PIPE-SL-025..180-40S
Command: `SSPIPE` schedule 40S

## Tab 03 Elbows
- SS-EL90LR-BW-{size}-10S / 40S
- SS-EL45LR-BW-{size}-10S / 40S
- SS-EL90SR-BW-{size}-40S
Command: `SSEL90` `SSEL45` `SSEL90S`

## Tab 04 Tees / reducers / caps
- SS-TEE-EQ-BW-{size}-10S / 40S
- SS-RED-CON-BW-{large}x{small}-40S
- SS-RED-ECC-BW-{large}x{small}-40S
- SS-CAP-BW-{size}-40S
Command: `SSTEE` `SSRED` `SSCAP`

## Tab 05 Flanges Cl.150
- SS-FLG-WN-150-{size}
- SS-FLG-SO-150-{size}
- SS-FLG-BL-150-{size}
- SS-FLG-LJ-150-{size}
Command: `SSFLG`

## Tab 06 Valves
- SS-VLV-BALL-FLG150-{size}
- SS-VLV-GATE-FLG150-{size}
- SS-VLV-GLB-FLG150-{size}
- SS-VLV-CHK-FLG150-{size}
- SS-VLV-BFY-WAFER-{size}
- SS-VLV-BALL-SW / THD for ≤2"
Command: `SSVALVE`

## Tab 07 Sanitary BPE
- SS-SAN-TUBE-{size}
- SS-SAN-EL90-TC-{size} / SS-SAN-EL45-TC-{size}
- SS-SAN-TEE-TC-{size}
- SS-SAN-RED-TC-{large}x{small}
- SS-SAN-TC-{size} (ferrule + clamp)
- SS-SAN-VLV-BALL-TC-{size}
- SS-SAN-VLV-DIA-TC-{size}
- SS-SAN-VLV-BFY-TC-{size}
Command: `SSTC` `SSSANEL` `SSSANTEE`

## Tab 08 P&ID symbols
- SS-PID-PIPE / EL90 / TEE / RED
- SS-PID-BALL / GATE / GLB / CHK / BFY / DIA
- SS-PID-FLG / TC / CAP / SPEC-BRK
Command: `SSPID`

## Tab 09 Annotation
- SS-ANNO-SIZE / SPEC / FLOW / SLOPE / INSUL
- SS-ANNO-MAT-304 / 316
- SS-ANNO-SCH-10S / 40S / SAN

## Tab 10 Pipe supports (additional package)
- SS-SUP-CLEVIS-{size}     MSS Type 1
- SS-SUP-CLAMP3-{size}     MSS Type 3
- SS-SUP-RISER-{size}      MSS Type 8
- SS-SUP-UBOLT-{size}      MSS Type 24
- SS-SUP-SLIDE-{size}      MSS Type 35
- SS-SUP-SADDLE-{size}     MSS Type 36/37
- SS-SUP-SHOE-{size}       welded T-shoe
- SS-SUP-DUMMY-{size}      dummy leg / trunnion
- SS-SUP-GUIDE-{size}
- SS-SUP-ANCHOR-{size}
- SS-SUP-TRAP-{size}       trapeze
- SS-SUP-WALL-{size}
- SS-SUP-SANHG-{size}      sanitary tube hanger
Command: `SSCLEVIS` `SSUBOLT` `SSSHOE` `SSDUMMY` `SSGUIDE` `SSANCHOR` `SSRISER` `SSTRAP` `SSSANHG` `SSSPACING`

## Tool properties to set after Create Tool Palette
- Prompt for rotation: Yes
- Explode: No
- Scale: 1
- Layer: as listed in Standards/LAYERS.md
- Aux scale: none (blocks are 1:1 inches)
