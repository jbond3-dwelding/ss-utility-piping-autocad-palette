# Block naming

Pattern:

```
SS-{FAMILY}-{TYPE}-{END}-{NPS}-{SCH}[-VIEW]
```

NPS token is two digits of inches with a leading zero when needed, fractions as 025 / 0375 / 050 / 075 / 100 / 125 / 150 / 200 …

Examples:

| Block | Meaning |
|---|---|
| SS-PIPE-BW-020-40S | 2" Sch 40S buttweld pipe segment |
| SS-EL90LR-BW-040-10S | 4" 90° long-radius BW elbow, Sch 10S |
| SS-EL45LR-BW-060-40S | 6" 45° LR BW elbow |
| SS-EL90SR-BW-020-40S | 2" 90° short-radius |
| SS-TEE-EQ-BW-030-40S | 3" equal tee |
| SS-RED-CON-BW-060x040-40S | 6x4 concentric reducer |
| SS-RED-ECC-BW-060x040-40S | 6x4 eccentric (FOB) |
| SS-CAP-BW-040-40S | 4" cap |
| SS-FLG-WN-150-040 | 4" Class 150 weld neck |
| SS-FLG-SO-150-040 | 4" Class 150 slip-on |
| SS-VLV-BALL-FLG150-040 | 4" flanged ball |
| SS-VLV-GATE-FLG150-060 | 6" flanged gate |
| SS-VLV-BFY-WAFER-080 | 8" wafer butterfly |
| SS-SAN-TUBE-020 | 2" BPE tube |
| SS-SAN-EL90-TC-020 | 2" sanitary 90 clamp |
| SS-SAN-TC-020 | 2" tri-clamp pair |
| SS-SUP-CLEVIS-040 | 4" MSS Type 1 clevis |
| SS-SUP-SHOE-080 | 8" pipe shoe |
| SS-PID-BALL | schematic ball valve |

Palette tools should Prompt for rotation = Yes, Explode = No, Scale = 1.
