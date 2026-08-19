# Vortex

### ▶ [Play it live](https://wesmcd6.github.io/vortex/)

A vector tube shooter in the Tempest tradition, in a **single self-contained HTML
file** — you ride the near rim of a wireframe web while everything hostile climbs
the lanes toward you. Twelve web shapes, six enemy types, a superzapper with two
uses, and a colour palette that cycles every level the way the cabinet did. No
build step, no dependencies, no server.

## Play it

Open `index.html` in any modern browser — that's the whole game.

```
xdg-open index.html      # Linux
open index.html          # macOS
start index.html         # Windows
```

Or serve the folder with any static server (e.g. `python3 -m http.server`).

## Controls

| Action | Keyboard | Touch |
|---|---|---|
| Move round the rim | `←` `→` (or `A` `D`) | left / right pads |
| Fire | `Space` (or `W`, `↑`) | FIRE pad |
| Superzapper | `Z` (or `Shift`) | fourth pad |
| Sound on/off | `M` | — |
| How to play | `H` | tap |
| Start / continue | `Space` or `Enter` | tap |

On a touch screen four pads appear along the bottom and can be held together.
All UI is drawn on the canvas, so phones never raise a selection or translate popup.

## The enemies

| | | |
|---|---|---|
| **Flipper** | red | Flips lane to lane as it climbs and hunts your position. At the rim it takes you if you're in its lane. |
| **Tanker** | purple | Slow and harmless until shot — then it splits into two of something worse in the lanes either side. |
| **Spiker** | green | Rides its lane spinning out a spike behind it. Shoot the spike down or it spears you during the warp. |
| **Fuseball** | orange | Rides the lane *edges* rather than the lanes, wandering sideways. Hard to hit, deadly at the rim. |
| **Pulsar** | blue | Periodically electrifies its whole lane. Don't be standing in it when it lights up. |

Tankers arrive at level 2, spikers at 3, fuseballs at 5, pulsars at 7, and from
level 6 a shot tanker splits into fuseballs or pulsars instead of flippers.

## Scoring

| Target | Points |
|---|---|
| Fuseball | 250 |
| Pulsar | 200 |
| Flipper | 150 |
| Tanker | 100 |
| Spiker | 50 |
| Spike segment | 1 |

Clearing a web is worth **level × 100**. An extra life every **20,000** points,
starting from three.

## The superzapper

Two charges per level, restored when the next web starts. The **first** use clears
the whole web. The **second** kills only the nearest thing, and then it's spent
until the next level — so the panic button gets weaker the moment you panic with it.

## The warp

Clear a web and you fly down the tube to the next one. Any spike still standing in
your lane kills you on the way through, so shoot them down *before* the last enemy
dies — once the web is clear it's too late to line one up.

## Faithful details

- **Twelve web shapes** cycling in order: circle, square, plus, flat, vee, triangle,
  star, double-v, hexagon, steps, clover, pentagon — open webs (flat, vee, steps,
  double-v) don't wrap, so the ends are dead ends you can be cornered against
- **Palette cycles per level**, six schemes of web / rim / accent colour
- **Seven shots** in flight at once
- Difficulty climbs on several axes at once: spawn cap, spawn rate, flip frequency,
  enemy fire rate and pulsar tempo all scale with level
- **Lives drawn as little claws** in the HUD, as on the original panel
- Vector look throughout — stroke-only rendering with beam glow, screen shake on
  death and a white flash on the superzapper, all honouring
  `prefers-reduced-motion`

## How it works

Everything is plain JavaScript on a `<canvas>`:

- Each web is a polygon or polyline **resampled to an exact segment count**, so any
  shape becomes a uniform set of lanes regardless of how it was drawn
- Lanes are projected from rim to far end through a depth curve, and enemies,
  shots and spikes are all positioned in `(lane, depth)` space and projected at
  draw time
- Fuseballs are tracked on lane *edges* rather than lane centres, which is what
  makes them awkward to hit
- Sound is synthesized live with the Web Audio API — no audio files
- The entire UI, including the how-to-play screen, is drawn on the canvas rather
  than in the DOM

## Disclaimer

This is an original, independent implementation written from scratch, inspired by
the classic vector tube-shooter genre. It is **not affiliated with, endorsed by, or
derived from Atari** or any other rights holder. No third-party code, artwork,
sounds, or other assets are used — all graphics are generated from vector
coordinates and all audio is synthesized at runtime. Any trademarks are the
property of their respective owners.

## License

Released under the [MIT License](LICENSE).
