# Nets Design System — reference for this prototype

Source: `Nets_Design-System`, file key `o2jAPzs7pH0etEDaVe7fAV`
Mobile screens live on the **"Mobile assorted"** canvas — node `1290:13857`.
Published library name: **Nets_Design System**.

Read from the file itself (variables, component instances), not guessed.

---

## Canvas size

Mobile screens in the DS are **360 × 800**.
This prototype renders at 390 × 844, so screenshots are not 1:1 with DS frames.

## Type

Family is **Assistant** throughout (Open Sans appears only inside avatar initials).

| Token | Spec |
|---|---|
| body M | Assistant Regular 16 / 20 |
| body M semibold | Assistant SemiBold 16 / 20 |
| body M bold | Assistant Bold 16 / 20 |
| body S | Assistant Regular 14 / 20 |
| body S semibold | Assistant SemiBold 14 / 20 |
| Caption 1 | Assistant Regular 12 |
| Caption 1 bold | Assistant Bold 12 |
| body XS regular | Assistant Regular 12 |

## Color tokens

| Token | Value |
|---|---|
| Primary/Dark Blue | `#1B293B` |
| Primary/White | `#FFFFFF` |
| Primary/Medium Blue | `#2C86F1` |
| **primary-cta/regular** | **`#2D85F2`** ← the CTA blue |
| Status/Green | `#52CC52` |
| Status/Red | `#F34545` |
| general/destructive | `#DB2626` |
| text/secondary | `#64748B` |
| general/border-light | `#CBD5E1` |
| Grays/Gray 5 | `#F4F4F5` |
| Grays/Gray 3 | `#D1D4D8` |
| Grays/Gray 1 | `#A4A9B1` |
| Grays/Gray Dark | `#767F89` |
| Shadow 1 | drop-shadow 0 4 7 `#0000002E` |

Palette ramps also present: red/100‑700, blue/100‑950, green/100‑700, yellow/100‑600,
orange/500, gray/200‑600.

Note there are **two blues**: `Primary/Medium Blue #2C86F1` (used for outlines, secondary
button text) and `primary-cta/regular #2D85F2` (filled CTAs, active nav item).

## Components — measured specs

### Buttons
| Component | Size | Radius | Padding | Text | Fill / Border |
|---|---|---|---|---|---|
| Mobile button primary L | 280×40 | **12** | 12/16 | Assistant Bold 16, white | solid fill |
| Mobile button tertiary L | 280×40 | 12 | 12/16 | Assistant Bold 16, `#64748B` | none |
| Mobile button secondary S | 105×32 | **8** | 6/10 | Assistant Regular 14, `#2C86F1` | 1px `#2C86F1`, no fill |

Other sizes exist: Mobile primary/secondary/tertiary in L/M/S, plus desktop
`Button primary|secondary|tertiary L|M|S` (132×40 for L).

**Secondary = outlined blue, not a grey fill.**

### Structure
| Component | Size | Notes |
|---|---|---|
| AppBar | 360×56 | white, bottom border `#F4F4F5`, padding 12/24, search placeholder Assistant Regular 16 `#A4A9B1` |
| bottom main nav | 360×72 | white, padding 0/20/8/20, labels Assistant Regular **14**; inactive `#64748B`, active `#2D85F2` |
| Inner Tabs / Inner Tab | 360×48 / 151×48 | |
| toast RTL | 320×48 | |
| mobile alarm card 28 | 324×130 | also variants 3, 4 at 320×84 |
| card | 360×41 | |

### Controls
| Component | Size | Notes |
|---|---|---|
| toggleswitch | 35×21 | radius 30, handle 14 (r7), gap 3.5; off `#CBD5E1`, on `#127FFF` |
| radio button | 24×24 | component set, `State=Checked/…` |
| badge | 16×16 | also `badge blue` |
| avatar with 3 indicators | 36×36 | plus 32/AvatarProfile 32×32, 24/Avatar Profile 24×24 |

---

## Where this prototype diverges from the DS

These are in `ptt-wireframe.html` and were invented before the DS was consulted:

| Prototype | Value | DS says |
|---|---|---|
| `--accent` | `#1f6f8b` teal | **not a DS colour.** DS map mic FAB is blue. Used here for the map mic, settings FAB, dock dots |
| `--ink` | `#26303a` | `#1B293B` Primary/Dark Blue |
| `--muted` | `#6b7684` | `#64748B` text/secondary (or `#767F89` Gray Dark) |
| `--line` | `#b8c0c9` | `#CBD5E1` border-light / `#D1D4D8` Gray 3 |
| `--danger` | `#c0453a` | `#F34545` Status/Red or `#DB2626` destructive |
| `--paper` | `#eef1f4` | no matching token |
| CTA radius | 10px | 12 (L) / 8 (S) |
| Empty-state CTA | `#2c86f1` | `#2D85F2` primary-cta/regular |

Already correct: Assistant font, `--cta #2d85f2`, `--gray5/3/1`, `--gray-dark`,
`--slate900`, `--text-secondary`, `--status-green`.

## Reference screens on the Mobile assorted canvas

`1291:15910` (m 3) is the map screen this prototype is based on. Others: m 4, m 5, m 11,
m 14, m 245, m 823, m 828, m 831‑833, plus `single emergency`, `mini-popup v1/v2`,
`household open`, and scenario sections (drone ID, sensor listening, etc.).

In the DS map screen the mic FAB is **blue**, there is a **chat-bubble FAB** above it,
the status card is more compact (two rows, meta line with author/time/source + an
`אמת` badge), and the tab bar carries **numeric badges**.
