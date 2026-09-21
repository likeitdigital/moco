# moco — character motion

A tiny character motion studio for expressive, living brand assets.

**[Open the studio →](https://likeitdigital.github.io/moco/app.html)** · [Project page](https://likeitdigital.github.io/moco/)

> **For the GitHub "About" field** (Settings → repo description, top right of the repo page):
> *A browser-based character motion studio for living brand systems — organic shapes,
> six states and eight motions, exported exactly as they look on screen.*
> Website field: `https://likeitdigital.github.io/moco/`

MOCO is an experimental, browser-based design tool for creating organic characters and
bringing them to life through shape, expression and motion. Choose a silhouette, define
its colour and state, arrange motions on a timeline, and export the result for use in
digital projects.

---

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

**Shape & colour** — six organic silhouettes, a curated pastel palette and any custom
colour. The face colour is derived from the brand colour rather than chosen separately,
so the character reads as one object instead of a face placed on a shape.

**A shape generator, not six presets** — the Blob shape is drawn rather than picked.
*Complexity* sets how many bulges the silhouette can have (3–12), *Character* how far
they go, and *Random shape* rolls a new seed — the shape then morphs into the new one
instead of snapping. Inspired by [blobmaker](https://www.blobmaker.app/);
`border-radius` only has four corners and cannot go this far.

Three things make the results abstract without falling apart. The radii come from a sum
of a few low-frequency waves rather than white noise, so bulges are wide instead of
spiking into single thorns. The outline is a centripetal Catmull-Rom curve, which
tolerates large radius jumps without overshooting or looping — plain uniform Catmull-Rom
produces kinks at these amplitudes. And each shape is recentred on its centroid and
refitted to the box, so an asymmetric silhouette still carries its face in the body.

The morph interpolates radii rather than paths, which keeps working when the point count
changes: the old set is resampled to the new length first.

Every shape is reproducible from three numbers, so it can be written down and reused:
*Blob, 7 points, character 65, seed 314* — and the filename carries them.

**States, not moods** — Idle, Hello, Thinking, Success, Oops and Attention. These are the
moments a product actually needs an asset for: empty states, loading, confirmation, error,
notice. Emoji-style emotions were deliberately dropped; they overlap and most of them are
unusable for a brand.

**Motion on a timeline** — eight motions, arranged by dragging. Selecting a motion previews
it; adding it to the timeline is a separate, deliberate step. Every clip runs whole cycles,
so each motion ends at rest and a sequence loops without a jump. Blink closes one eye
rather than both — a wink reads as alive, two shut eyes read as switched off. On the
Hello state, where one eye is already winking, Blink opens that eye instead of closing
the other.

**Export** — PNG (1024 × 1024, transparent), SVG, and animated SVG. The export reflects the
exact state on screen: shape, colour, state, size and the full motion sequence. The animated
file is periodic, so it loops seamlessly wherever it is embedded.

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
time. The preview was right, the file was not. Several other faults were invisible in the
interface too: the size control was silently overridden by every motion, and the exported
animation jumped on each loop.

That experience became a short German guide, **Der Funktionsbeweis** — five levels on which
to check whether a prototype actually works, available at
[likeit.digital](https://likeit.digital).

---

## On phones

The phone layout is an app screen, not a scrolled-down desktop page. Nothing scrolls:
header on top, stage filling the space between, one panel as a sheet over the stage,
and a tab bar of seven single-purpose sections at the bottom — Shape, Color, Size, Blob,
Motion, Face, Time. Picking the Blob silhouette jumps straight to its controls, and the
chosen section is remembered between visits.

The stage reports the open sheet's height back into its own padding, so the character
centres in the space that is actually visible instead of sitting half behind the sheet.
Each sheet reaches all the way down to the tab bar rather than floating above it with a
gap — for the panels that live inside the workspace that means anchoring to its own
edge, which already sits flush on the bar; the timeline sits outside the stage in the
markup as a sibling of the tab bar, so it anchors to the app frame instead and keeps the
bar's own height as clearance — without that shared anchor it ended up behind the bar
with its button no longer tappable.

Stacking every panel made the page 1787 pixels tall and pushed the character out of view
while its own controls were being used. Now everything fits one screen.

Export sits in the header, top right. The footer is hidden here; its links belong to the
project page, not to the tool.

Within each panel the pickers are horizontally scrolling rows, with enough inner spacing
for the selection outline and matching `scroll-padding` — without it the snap pulls the
first item flush to the edge and cuts its outline off. Touch targets are at least 40px
throughout.

The blob outline is drawn at the element's real size rather than a fixed one. `clip-path`
works in absolute pixels, and the character box is smaller on phones than on desktop — with
a fixed path the shape was cut off on the right and bottom. Each shape is also scaled up to
fill its box after being centred, instead of only ever being scaled down.

Between 760 and 1250 pixels there are no tabs; the export button moves into the header
instead, because the layout hides the one in the timeline at that width — without it
there would be no way to export at all in that range.

---

## Running it

No build step, no dependencies. Two files:

- `index.html` — the project page
- `app.html` — the studio itself

Open `app.html` in a browser, or host the folder anywhere static.

---

Concept, UX/UI & character design by **[likeit.digital](https://likeit.digital)**

MOCO is an independent design experiment by Cornelia Hermine Süß / likeit.digital.
