# Particle Type

**Type anything. Watch thousands of glowing particles fly into place and spell it out.**

Particle Type is an interactive typography toy that runs in the browser. Every letter is made of thousands of small particles, and each one is pulled toward its spot by a spring. Move your cursor through the words and the particles swirl away, then drift back. Click and the text shatters, then pulls itself back together.

It's one HTML file with no frameworks, no build step and no dependencies. Just the Canvas 2D API and some physics.

**▶ Live demo:** https://jackthecoder17.github.io/particle-type/

---

## Features

- **Type anything:** the particles morph into new text as you type. Long phrases wrap onto up to three lines automatically.
- **Cursor physics:** the cursor pushes particles outward with a slight swirl, so it stirs the letters instead of punching holes in them.
- **Click to shatter:** a radial burst from wherever you click, followed by a springy reassembly.
- **Space to scatter:** throws every particle in a random direction.
- **4 palettes:** Ember, Aurora, Tide and Candy, each applied as a diagonal colour sweep across the word.
- **Glowing trails:** additive blending plus a translucent fade between frames gives the motion-blur look. You can toggle it off.
- **Demo mode:** cycles through phrases by itself. Good for a background tab or a screen recording.
- **Adaptive:** the particle count (2,500–9,000) scales to your screen size, it's sharp on retina displays, and it works with touch on phones.
- **Accessible:** respects `prefers-reduced-motion`, and every control works from the keyboard.

## How it works

1. **Rasterise the text.** The text is drawn onto a hidden canvas at the largest size that fits the screen.
2. **Sample the pixels.** The hidden canvas is scanned on a grid, and every filled pixel becomes a target point. The grid spacing is tuned so the number of points roughly matches the number of particles, and a little jitter keeps the letters from looking like a grid.
3. **Assign targets.** Particles are shuffled before they get their new targets, so each morph takes a different path.
4. **Simulate each frame.** Every particle feels a spring force toward its target, a repulsion-plus-swirl force near the cursor, and damping. Positions live in `Float32Array`s to keep the loop fast.
5. **Batch the drawing.** Particles are grouped by colour so the canvas changes `fillStyle` only once per colour per frame. That keeps it at 60 fps with thousands of particles.

## Run it locally

```bash
git clone https://github.com/jackthecoder17/particle-type.git
cd particle-type
open index.html
```

Or serve it with any static server, for example `npx serve .`.

## Customise it

Everything is in `index.html`:

| What | Where |
| --- | --- |
| Demo phrases | the `DEMO` array |
| Colour palettes | the `PALETTES` object (add your own) |
| Springiness / friction | `spring` and `damp` in `frame()` |
| Cursor radius and strength | `R` and the `6 * dt` force in `frame()` |
| Particle count | `targetCount()` |

## Tech

HTML · CSS · vanilla JavaScript · Canvas 2D · Google Fonts (Unbounded, JetBrains Mono)

## License

MIT. Fork it, remix it, put your name in particles.
