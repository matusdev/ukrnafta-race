# Landing backgrounds: hero + AZK (2.5D parallax)

Source: `project - ukrnafta/design/2.png` (1487×1058). The two photo bands were cropped strictly inside the photo area. The baked-in UI was inpainted away, then each band was upscaled 2× (lanczos3 + mild unsharp).
Depth: Depth Anything V2 small (transformers.js). Bright = near, dark = far, same convention as `menu_depth.png`, so the `menuscene.ts` shader works unchanged (`uv + uOff * (depth - 0.35)`).

| file | px | aspect | bytes |
|---|---|---|---|
| hero_bg.jpg / .webp | 2508×1412 | 1.776 : 1 | 481 854 / 356 418 |
| hero_depth.png (8-bit gray) | 836×471 (half) | 1.776 : 1 | 48 309 |
| azk_bg.jpg / .webp | 2974×462 | 6.437 : 1 | 231 999 / 152 902 |
| azk_depth.png (8-bit gray) | 1487×231 (half) | 6.437 : 1 | 52 340 |

Crop rows in 2.png: hero = y 0–329, AZK = y 541–771 (full width).

All coordinates below are normalised: x = 0 at the left edge, y = 0 at the top.

## hero_bg (replaced 2026-11-02)
Client key art (1672×941, 16:9): the UKRNAFTA station at night in the rain, a yellow route minibus under the canopy,
wet asphalt in the front third. Upscaled 1.5× to 2508×1412 (lanczos3 + mild unsharp); depth at half size (836×471).
The previous band art is kept in `_not_main/hero_old/` with the client's source PNG.
- **Layout:** the hero is cover-fitted (no band mode any more), focus x 0.60 / y 0.55 (the bus and the canopy).
- **Text zone:** x < 0.30 (trees, the street, the dark sky); the pylon is at x ≈ 0.32–0.37, the canopy from x ≈ 0.40.
- **Depth:** sky and the station far (dark), the asphalt near (bright towards the bottom), the tree top left near.

## azk_bg
- **Ground / horizon:** the car wheels and the forecourt edge are at y ≈ 0.84–0.87. Wet asphalt runs from y ≈ 0.85 to the bottom. The base of the far tree line is at y ≈ 0.80.
- **Main subject:** canopy x 0.43–0.80; the canopy logo is at x 0.46–0.51. Shop with a second "UKRNAFTA" sign x 0.66–0.90, "Market" sign at about x 0.87. Yellow bus x 0.36–0.43, sedans x 0.43–0.49 and x 0.63–0.70. The station occupies **x ≈ 0.36–0.92**, centred near x 0.62.
- **Text zone:** x < 0.35 is a very dark (designer-darkened) inpainted park with a row of parked cars at y ≈ 0.62–0.85.
- **Depth values:** dark left area about 0.19, bus 0.36, canopy 0.39, shop 0.32, sedan 0.48, ground at y 0.92 ≈ 0.67, bottom ≈ 0.95.

## Parallax tips
`menuscene.ts` drives `uOff` up to (0.02, 0.012) in UV units. Relative to their height, these bands are 2.5× (hero) and 3.6× (AZK) wider than the menu image (1.78 : 1), so the same UV offset moves more pixels in x. About 0.010–0.015 in x looks equivalent and stays clean.
A test at ±0.03 shows only mild, smooth stretching on the side of the pylon and sedan edges that the movement uncovers, with no tearing.
