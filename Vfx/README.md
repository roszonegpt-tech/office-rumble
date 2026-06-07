# VFX Assets

Place visual effect sprite sheets and particle textures here.

## Expected Files

| File | Description |
|------|-------------|
| `hit_spark.png` | Hit flash effect (4-frame horizontal strip) |
| `dust_cloud.png` | Dust puff on landing (4-frame strip) |
| `energy_burst.png` | Super move energy burst (8-frame strip) |
| `blood_splat.png` | Optional impact splat (4-frame strip) |

## Sprite Sheet Format

All VFX sheets use the same horizontal strip format as character sprites:
- Each frame is **64×64 px**
- Frames are arranged left-to-right in a single row
- PNG with transparency (alpha channel required)
- 72 DPI, RGB + Alpha

## Updating Sprites

To add a VFX sheet, drop the PNG here and reference it in `js/game.js` inside
the `VFX_SHEETS` constant (or wherever the effect is loaded). The engine loads
it as a Three.js `TextureLoader` texture mapped onto a billboard mesh.

## Character Sprite Sheets

Character sprite atlases are stored as base64 data URIs inside `js/sprites.js`.
Each character key (`c1`–`c5`) maps to a 32-frame horizontal strip
(6144×240 px, **192×240 px per frame**):

| Frames | Action |
|--------|--------|
| 0 | IDLE |
| 1–3 | WALK A/B/C |
| 4–5 | RUN A/B |
| 6–7 | JUMP A/B |
| 8 | DUCK |
| 9 | BLOCK |
| 10–13 | PUNCH A/B/C/D |
| 14–17 | KICK A/B/C/D |
| 18–19 | JUMP KICK A/B |
| 20–21 | DUCK PUNCH A/B |
| 22–25 | SPECIAL A/B/C/D |
| 26 | HIT (take damage) |
| 27–28 | TAUNT / WIN A/B |
| 29–31 | DIE / KO A/B/C |

Frames are laid out left-to-right with the figure's feet anchored to the bottom
of each cell, a consistent scale across all frames, all facing **right** (the
engine mirrors automatically for left-facing fighters).

To replace a sprite sheet, open `js/sprites.js`, find the relevant character key,
and replace the base64 string with the output of:

```bash
base64 -w 0 your_sprite.png
# then wrap it: "data:image/png;base64,<output>"
```
