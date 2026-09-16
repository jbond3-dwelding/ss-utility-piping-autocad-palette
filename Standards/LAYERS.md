# Layer standard — SS Utility / Process Piping

NCS-aligned. Discipline **P** = Process / piping. Major groups PIPE / FITT / VALV / SAN / SUPP.

| Layer | Color | Linetype | Plot | Use |
|---|---|---|---|---|
| P-PIPE-CONT | 4 cyan | CONTINUOUS | 0.50 | Process / utility pipe OD (double-line) |
| P-PIPE-CNTR | 2 yellow | CENTER2 | 0.18 | Pipe centerline |
| P-PIPE-HIDD | 8 grey | HIDDEN2 | 0.18 | Hidden / far wall |
| P-FITT-CONT | 6 magenta | CONTINUOUS | 0.50 | Elbows, tees, reducers, caps |
| P-VALV-CONT | 1 red | CONTINUOUS | 0.50 | Valves |
| P-FLNG-CONT | 5 blue | CONTINUOUS | 0.50 | Flanges |
| P-SAN-CONT | 3 green | CONTINUOUS | 0.50 | BPE tube, ferrules, clamps |
| P-SAN-GASK | 3 green | HIDDEN2 | 0.18 | Gasket / clamp outline |
| P-SUPP-CONT | 8 grey | CONTINUOUS | 0.35 | Hangers, shoes, guides |
| P-SUPP-ROD | 8 grey | CONTINUOUS | 0.25 | Hanger rod |
| P-ANNO-TEXT | 7 white | CONTINUOUS | 0.25 | Tags, sizes, notes |
| P-ANNO-PID | 7 white | CONTINUOUS | 0.25 | P&ID symbols |
| P-PIPE-INSUL | 30 | HIDDEN2 | 0.18 | Insulation OD |
| Defpoints | 7 | CONTINUOUS | off | Construction inside blocks |

Aliases created by SSSETUP for short names used in older drafts:
`SS-PIPE` `SS-FITTING` `SS-VALVE` `SS-SAN` `SS-SUPPORT` `SS-ANNO` `SS-CENTER`

Text style: **SS-ANNO** — romans.shx, height 0.125 in model.
Dim style: decimal inches, 0.00, closed filled arrow.

Block attributes (every pipe / fitting / valve):
`TAG SIZE SCH MATL END RATING SPEC VIEW NOTES`
