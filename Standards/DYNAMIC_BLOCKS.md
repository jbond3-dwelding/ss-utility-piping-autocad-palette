# Dynamic block specification — SS Utility / Process Piping

True AutoCAD Dynamic Blocks live in proprietary DWG evaluation graphs
(BEDIT parameters + actions + lookup tables). This package cannot emit
those dictionaries from LISP/DXF. Use this recipe to promote a prototype
block after `SSLIB` draws it.

## Master families (one block each)

| Master block | Lookup keys | Visibility states | Stretch / other |
|---|---|---|---|
| SS-PIPE-DYN | SIZE, SCH (10S/40S/SAN) | PLAN, ELEV, SINGLELINE | Linear LEN on both OD lines |
| SS-ELL-DYN | SIZE, SCH, RADIUS (LR/SR/3D), ANGLE (45/90/180) | — | Polar rotate; Flip inlet |
| SS-TEE-DYN | SIZE, BRANCH, SCH | EQUAL, REDUCING | Flip branch |
| SS-RED-DYN | LARGE, SMALL, SCH | CONC, ECC-FOB, ECC-FOT | Linear LENGTH = B16.9 H |
| SS-FLG-DYN | SIZE, CLASS (150), TYPE | WN, SO, LJ, THD, BLIND | — |
| SS-VLV-DYN | SIZE, END, PATTERN | GATE, GLOBE, BALL, CHECK, BFLY, PLUG | Linear FTF from B16.10; Flip flow |
| SS-SAN-DYN | TUBE-OD | TUBE, EL90, EL45, TEE, FERRULE, CLAMP, BALL, BFLY | — |
| SS-SUP-DYN | SIZE | CLEVIS, UBOLT, SHOE, RISER, GUIDE, ANCHOR, TRAPEZE, SANHGR | — |

Shared attributes on every master: `TAG SIZE SCH MATL END RATING SPEC VIEW NOTES`

Default MATL = `304/304L`. Change to `316/316L` per spec.

## BEDIT conversion recipe

1. Run `SSSETUP` then draw a **2" Sch 40S** prototype of the family (`SSPIPE`, `SSEL90`, `SSVALVE`, …).
2. `BLOCK` it as the master name above. Base point = fitting center or pipe start. Centerline on Y=0. Flow +X.
3. `BEDIT` the master.
4. Parameters tab:
   - **Linear** parameter along the run (pipe length or valve face-to-face). Add a Stretch action to both OD lines and end ticks.
   - **Lookup** parameter. Properties table columns = SIZE + SCH (and END / TYPE as needed).
   - **Visibility** parameter for family variants (valve type, conc/ecc, plan/elev).
   - **Flip** parameter on the X axis (flow / eccentric flat-on-bottom).
   - **Rotation** parameter, increment 90°, if the tool will not use "Prompt for rotation".
5. Fill the lookup table from `Standards/PIPE_DIMENSIONS.csv`, `FITTINGS.csv`, `VALVES.csv`, `SANITARY.csv`.
   - SIZE list: 1/4 3/8 1/2 3/4 1 1-1/4 1-1/2 2 2-1/2 3 3-1/2 4 5 6 8 10 12 14 16 18
   - Each row sets custom properties OD, WT, A/B/C/H/FTF used by constraints or by a user-variable scale of the prototype.
6. Constraint idea that stays robust: keep geometry drawn at **1" nominal OD = 1.000**, then use a Scale action driven by the OD property. Do **not** scale text attributes.
7. `BTEST` grips. Save. `WBLOCK` to `Blocks/SS-PIPE-LIBRARY.dwg`.
8. Design Center → Create Tool Palette. Set Prompt for rotation = Yes, Explode = No, Scale = 1.

## Lookup columns to paste into BEDIT

### Pipe (B36.19M)

SIZE | OD | WT_10S | WT_40S | OD_SAN | WT_SAN
---|---|---|---|---|---
1/4 | 0.540 | 0.065 | 0.088 | 0.250 | 0.035
3/8 | 0.675 | 0.065 | 0.091 | 0.375 | 0.035
1/2 | 0.840 | 0.083 | 0.109 | 0.500 | 0.065
3/4 | 1.050 | 0.083 | 0.113 | 0.750 | 0.065
1 | 1.315 | 0.109 | 0.133 | 1.000 | 0.065
1-1/4 | 1.660 | 0.109 | 0.140 | — | —
1-1/2 | 1.900 | 0.109 | 0.145 | 1.500 | 0.065
2 | 2.375 | 0.109 | 0.154 | 2.000 | 0.065
2-1/2 | 2.875 | 0.120 | 0.203 | 2.500 | 0.065
3 | 3.500 | 0.120 | 0.216 | 3.000 | 0.065
3-1/2 | 4.000 | 0.120 | 0.226 | — | —
4 | 4.500 | 0.120 | 0.237 | 4.000 | 0.083
5 | 5.563 | 0.134 | 0.258 | — | —
6 | 6.625 | 0.134 | 0.280 | 6.000 | 0.109
8 | 8.625 | 0.148 | 0.322 | 8.000 | 0.109
10 | 10.750 | 0.165 | 0.365 | 10.000 | 0.109
12 | 12.750 | 0.180 | 0.375 | 12.000 | 0.109
14 | 14.000 | 0.188 | 0.375 | — | —
16 | 16.000 | 0.188 | 0.375 | — | —
18 | 18.000 | 0.188 | 0.375 | — | —

NPS 12 40S wall is **0.375** (B36.19M), not B36.10 Sch 40 0.406.
NPS 14–18 10S wall is **0.188**, not B36.10 Sch 10 0.250.

### Elbow / tee / cap (B16.9 inches)

SIZE | A_90LR | B_45LR | A_90SR | TEE_C | CAP_E
---|---|---|---|---|---
1/2 | 1.50 | 0.62 | — | 1.00 | 1.00
3/4 | 1.50 | 0.75 | — | 1.12 | 1.00
1 | 1.50 | 0.88 | 1.00 | 1.50 | 1.50
1-1/4 | 1.88 | 1.00 | 1.25 | 1.88 | 1.50
1-1/2 | 2.25 | 1.12 | 1.50 | 2.25 | 1.50
2 | 3.00 | 1.38 | 2.00 | 2.50 | 1.50
2-1/2 | 3.75 | 1.75 | 2.50 | 3.00 | 1.50
3 | 4.50 | 2.00 | 3.00 | 3.38 | 2.00
3-1/2 | 5.25 | 2.25 | 3.50 | 3.75 | 2.50
4 | 6.00 | 2.50 | 4.00 | 4.12 | 2.50
5 | 7.50 | 3.12 | 5.00 | 4.88 | 3.00
6 | 9.00 | 3.75 | 6.00 | 5.62 | 3.50
8 | 12.00 | 5.00 | 8.00 | 7.00 | 4.00
10 | 15.00 | 6.25 | 10.00 | 8.50 | 5.00
12 | 18.00 | 7.50 | 12.00 | 10.00 | 6.00
14 | 21.00 | 8.75 | 14.00 | 11.00 | 6.50
16 | 24.00 | 10.00 | 16.00 | 12.00 | 7.00
18 | 27.00 | 11.25 | 18.00 | 13.50 | 8.00

Reducer end-to-end H is keyed to the **large** NPS: 3/4=1.50, 1=2.00, 1-1/4=2.00, 1-1/2=2.50, 2=3.00, 2-1/2=3.50, 3=3.50, 3-1/2=4.00, 4=4.00, 5=5.00, 6=5.50, 8=6.00, 10=7.00, 12=8.00, 14=13.00, 16=14.00, 18=15.00.

### Valve Class 150 face-to-face (B16.10 inches)

SIZE | GATE / BALL-SP | GLOBE / SWING-CHECK | BFLY WAFER (narrow)
---|---|---|---
1/2 | 4.25 | 4.25 | —
3/4 | 4.62 | 4.62 | —
1 | 5.00 | 5.00 | —
1-1/4 | 5.50 | 5.50 | —
1-1/2 | 6.50 | 6.50 | 1.31
2 | 7.00 | 8.00 | 1.69
2-1/2 | 7.50 | 8.50 | 1.81
3 | 8.00 | 9.50 | 1.81
4 | 9.00 | 11.50 | 2.06
5 | 10.00 | 13.00 | 2.19
6 | 10.50 | 16.00 | 2.19
8 | 11.50 | 19.50 | 2.38
10 | 13.00 | 24.50 | 2.69
12 | 14.00 | 27.50 | 3.06
14 | 15.00 | 31.00 | 3.06
16 | 16.00 | 36.00 | 3.12
18 | 17.00 | 39.00 | 4.00

Ball long-pattern at 6" and up is longer (6"=15.50). Default the lookup to short pattern; add a PATTERN column if you stock both.

### Sanitary clamp flange OD (BPE / 3-A)

TUBE | FERRULE_OD | WALL
---|---|---
1/4 3/8 1/2 3/4 | 0.984 | 0.035 (1/4, 3/8) or 0.065
1 and 1-1/2 | 1.984 | 0.065
2 | 2.516 | 0.065
2-1/2 | 3.047 | 0.065
3 | 3.579 | 0.065
4 | 4.682 | 0.083
6 | 6.562 | 0.109

1" and 1-1/2" share a ferrule. Do not size clamps by flange OD.

### MSS SP-58 Table 4 spacing + Table 3 rod

SIZE | WATER_FT | VAPOR_FT | MIN_ROD
---|---|---|---
1/4 | 5 | 5 | 3/8
3/8–1-1/4 | 7 | 8–9 | 3/8
1-1/2 | 9 | 12 | 3/8
2 | 10 | 13 | 3/8
2-1/2 | 11 | 14 | 1/2
3 | 12 | 15 | 1/2
3-1/2 | 13 | 16 | 1/2
4 | 14 | 17 | 5/8
5 | 16 | 19 | 5/8
6 | 17 | 21 | 3/4
8 | 19 | 24 | 7/8
10 | 22 | 26 | 7/8
12 | 23 | 30 | 7/8
14 | 25 | 32 | 1
16 | 27 | 35 | 1
18 | 28 | 37 | 1-1/8

Sch 10S sags more than STD wall. Use ~85% of Table 4 unless a span calculation is performed. Add supports at concentrated loads (valves, flanges) and direction changes regardless of the table.

## Grip and insertion convention

- Origin = pipe start **or** fitting / valve centerline intersection.
- Centerline on Y = 0. Flow +X. Branch of tee +Y.
- Eccentric reducer: flat-on-bottom is the default visibility; flip to flat-on-top.
- Palettes: Prompt for rotation = Yes so one block covers plan north/east/south/west.

## What LISP already does instead

`SSPIPE` `SSEL90` `SSVALVE` `SSTC` `SSCLEVIS` (and the other family commands) look up the same numbers and draw to-scale geometry. That is the supported workflow until a master is promoted in BEDIT. `SSLIB` / `SSSUPLIB` bake one block per size for Design Center → Create Tool Palette.
