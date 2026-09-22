
# moco — character motion

A tiny character motion studio for expressive, living brand assets.

MOCO is an experimental, browser-based design tool for creating organic characters and
bringing them to life through shape, expression and motion. Choose a silhouette, define
its colour and state, arrange motions on a timeline, and export the result for use in
digital projects.

---
<img width="2000" height="1403" alt="screenshot-desktop" src="https://github.com/user-attachments/assets/42eaf76a-7c0b-48f0-b96d-4390f8447d41" />
## Why MOCO?

Brand assets don't have to be static.

MOCO explores the idea of **living brand systems** — visual identities in which motion,
behaviour and expression become part of the design language rather than something added
afterwards by someone else.

Instead of delivering a fixed collection of files, a designer can define a system that
allows new variations to be created while staying inside the visual language of the brand.
The client gets the studio, not just the output.

> Brand guidelines can become interfaces.

---

## What it does

### Organic shapes

The Blob shape is drawn rather than picked. *Complexity* sets how many bulges the
silhouette can have (3–12), *Character* how far they go, and *Random shape* rolls a new
seed — the shape then morphs into the new one instead of snapping. Inspired by
[blobmaker](https://www.blobmaker.app/); `border-radius` only has four corners and cannot
go this far.

The radii come from a sum of a few low-frequency waves rather than white noise, so bulges
stay wide instead of spiking into single thorns, and the outline itself is a centripetal
Catmull-Rom curve, which tolerates large radius jumps without overshooting or looping —
plain uniform Catmull-Rom kinks at these amplitudes. Each shape is recentred on its
centroid and refitted to the box, so an asymmetric silhouette still carries its face in
the body.

Every shape is reproducible from three numbers, so it can be written down and reused:
*Blob, 7 points, character 65, seed 314* — and the filename carries them.

The face colour is derived from the brand colour rather than chosen separately, so the
character reads as one object instead of a face placed on a shape.

### Product states

Idle, Hello, Thinking, Success, Oops and Attention — the moments a product actually needs
an asset for: empty states, loading, confirmation, error, notice. Emoji-style emotions
were deliberately dropped; they overlap and most of them are unusable for a brand.

### Motion

Eight motions, arranged on a timeline by dragging. Selecting a motion previews it; adding
it to the timeline is a separate, deliberate step. Every clip runs whole cycles, so each
motion ends at rest and a sequence loops without a jump. Blink closes one eye rather than
both — a wink reads as alive, two shut eyes read as switched off. On the Hello state,
where one eye is already winking, Blink opens that eye instead of closing the other.

The morph between shapes interpolates radii rather than paths, which keeps working when
the point count changes: the old set is resampled to the new length first.

### Export

PNG (1024 × 1024, transparent), SVG, and animated SVG. The export reflects the exact state
on screen: shape, colour, state, size and the full motion sequence. The animated file is
periodic, so it loops seamlessly wherever it is embedded.

---

## Design principles

MOCO is intentionally small and focused.

Motion should feel subtle rather than decorative. Shapes should stay organic. Controls
should be understandable without turning the experience into an animation application.

The goal is not to replace professional motion-design software, but to explore how motion
can become a native part of a brand system.

---

## Built as a design experiment

MOCO started from a broader question:

> What happens when designers don't just create the assets — but also create the tools
> that generate them?

Rapid prototyping and AI-assisted development make it possible to move from designing
individual outputs towards designing the rules, behaviours and interfaces behind those
outputs. That opens an interesting space between branding, product design and creative
tooling.

The most instructive part turned out to be the testing. The first working version looked
finished and behaved correctly on screen — and exported the wrong character every single
time. The preview was right, the file was not. A prototype can look finished and still be
functionally wrong in ways the interface never shows: the size control here was silently
overridden by every motion, and the exported animation jumped on each loop.

That experience became a short guide, **Der Funktionsbeweis / Proof It Works** — five
levels on which to check whether a prototype actually works.

→ [Read the guide on likeit.digital](https://likeit.digital)

---

## Running it

No build step, no dependencies. Two files:

- `index.html` — the project page
- `app.html` — the studio itself

Open `app.html` in a browser, or host the folder anywhere static.

---

Concept, UX/UI & character design by **[likeit.digital](https://likeit.digital)**

MOCO is an independent design experiment by Cornelia Süß / likeit.digital.
