# Stainless Steel Utility / Process Piping Tool Palette for AutoCAD

2D CAD library for **all-stainless utility and process piping**, fittings, valves, sanitary tubing, and a separate **pipe-supports** package.

**Units:** 1 drawing unit = 1 inch. Insert at 1:1.
**Prefix:** `SS-`
**Material default:** ASTM A312 / A403 / A182 Type 304/304L (switch MATL attribute to 316/316L).

This is a layout / design library. It is **not** a licensed copy of ASME, MSS, or any OEM catalog. Verify every dimension against the current edition of the cited standard and the selected manufacturer before fabrication or purchase.

## What you get

| Folder | Contents |
|---|---|
| `Lisp/` | AutoLISP that creates layers and draws parametric plan/elevation blocks |
| `Python/` | R12 DXF generator (no extra packages) |
| `Dxf/` | Ready-to-import 2D symbols (run the Python generator) |
| `Palettes/` | Tab inventory and tool list for Design Center |
| `Standards/` | Layers, naming, pipe / fitting / valve / sanitary / support tables |

## Coverage

- **Sizes:** 1/4", 3/8", 1/2", 3/4", 1", 1-1/4", 1-1/2", 2", 2-1/2", 3", 3-1/2", 4", 5", 6", 8", 10", 12", 14", 16", 18"
- **Pipe:** ASME B36.19M Schedule **10S** and **40S** (palette labels also accept Sch 10 / Sch 40)
- **Sanitary:** ASME BPE / ASTM A270 OD tubing 1/4"–6" plus 8" extra, tri-clamp ferrules
- **Fittings:** B16.9 BW LR/SR 90, LR 45, equal tee, concentric/eccentric reducer, cap; B16.11 SW/THD; B16.5 Cl.150 WN/SO/BL/LJ
- **Valves:** ball, gate, globe, check, butterfly, sanitary ball / diaphragm / butterfly (typical F-F)
- **Supports package:** MSS SP-58 Types 1, 3, 8, 24, 35, 36/37, 39, 40, 41/43 plus process shoes, dummy legs, guides, anchors, trapeze, wall brackets, sanitary hangers

## Commands (after APPLOAD)

| Command | What it does |
|---|---|
| `SSSETUP` | Layers + SS-ANNO text style |
| `SSPIPE` | Double-line pipe run, size + schedule lookup |
| `SSEL90` `SSEL45` `SSEL90S` | 90 LR, 45 LR, 90 SR elbow |
| `SSTEE` `SSRED` `SSCAP` | Tee, reducer, cap |
| `SSFLG` | Class 150 flange (WN / SO / BL) |
| `SSVALVE` | Ball / gate / globe / check / butterfly |
| `SSTC` `SSSANEL` `SSSANTEE` | Tri-clamp, sanitary 90, sanitary tee |
| `SSPID` | P&ID symbol (not to-scale) |
| `SSLIB` | Build size-specific blocks in the current drawing |
| `SSHELP` | Command list |
| `SSCLEVIS` `SSUBOLT` `SSSHOE` `SSDUMMY` | Support package |
| `SSGUIDE` `SSANCHOR` `SSRISER` `SSTRAP` | Support package |
| `SSSANHG` `SSSPACING` | Sanitary hanger + MSS span table |
| `SSSUPLIB` | Build support blocks |

## Install in AutoCAD (fastest path)

1. Copy this folder to a stable path, preferably UNC:
   `\\Server\\CAD\\SS_Utility_Piping_ToolPalette\\`
   or `C:\\CAD\\SS_Utility_Piping_ToolPalette\\`
2. `APPLOAD` → load `Lisp/SS-Piping.lsp` and `Lisp/SS-Supports.lsp`.
   Check *Startup Suite* so they load every session.
3. Type **SSSETUP** then **SSLIB** then **SSSUPLIB**.
4. Save as `Blocks/SS-PIPE-LIBRARY.dwg` (and `Blocks/SS-SUPPORT-LIBRARY.dwg` if you split).
5. `ADCENTER` (Ctrl+2) → browse to that DWG → **Blocks** → right-click → **Create Tool Palette**.
6. Split tools onto the tabs listed in `Palettes/PALETTE_CATALOG.md`. Add separators and text labels.
7. `CUSTOMIZE` → drag palettes into a group named **SS Utility Piping** → right-click group → **Export** `.xpg`.
8. Right-click each palette → **Export** `.xtp` into `Palettes/`.
9. OPTIONS → Files → add the folder to **Support File Search Path** and **Tool Palettes File Locations**.

### Import DXF symbols without LISP

```
python Python/generate_dxf.py Dxf
```

Then `INSERT` or Design Center each file in `Dxf/`.

### AutoCAD Architecture / MEP

Those products cannot Import `.xtp`. Use Content Browser and an `.atc` catalog, or drag blocks from Design Center onto an existing palette.

## Dynamic blocks — honest limit

True AutoCAD Dynamic Blocks (visibility states, stretch actions, lookup tables inside BEDIT) are proprietary DWG dictionaries. This package ships the **parametric equivalent**:

- LISP commands that look up ASME / BPE / MSS dimensions and draw at the selected size
- Size-specific blocks (`SS-EL90LR-BW-04-40S`) you drop on a palette
- Attributes: `TAG SIZE SCH MATL END RATING SPEC VIEW NOTES`
- A conversion recipe in `Standards/DYNAMIC_BLOCKS.md` if you want to promote a master block to BEDIT visibility + lookup

## Important XTP facts

- An `.xtp` does **not** contain geometry. It stores labels, layer/scale/rotation properties, and a **Source File** path to the DWG.
- Icons live in a sibling `Images\\` folder created on Export. Keep XTP + Images together.
- If tools go blank after a move: right-click tool → Properties → Source File → repath to the library DWG.
- Do not hand-author XTP XML. GUIDs and stock-tool refs break easily.

## Legal / use

Layout symbols and published-dimension lookups only. Confirm wall, face-to-face, clamp, and support load data against:
ASME B36.19M, B16.9, B16.11, B16.5, B16.10, B16.34, B31.3, ASME BPE, 3-A, MSS SP-58, and the valve / hanger manufacturer.
