#  Interactive 3D Scroll Portfolio

A single-page, scroll-driven 3D portfolio by **Disha Mohnani**. A paper airplane flies through three themed classrooms (an **electronics lab**, an **app development room**, and a **creative studio**) while hand-drawn notebook cards fade in to tell the story of her research, competitions, projects, and community work.

Everything lives in one `index.html` file. There is no build step and nothing to install.

---

## Highlights

- **Scroll-controlled flight.** Scrolling moves a paper airplane along a smooth 3D spline path through the scene. The camera follows with eased motion and a subtle mouse parallax.
- **Fully procedural 3D world.** Classrooms, benches, desks, laptops, easels, windows, sunbeams, and wall posters are built from Three.js primitives. Poster textures are drawn at runtime on `<canvas>` elements, so there are no image or model files.
- **Notebook-paper UI.** Content cards look like ruled paper with tape, handwritten fonts, highlighter marks, and a "writing" reveal animation for each line.
- **Interactive hotspots.** Pulsing `+` markers on the electronics bench, app desk, easel, and book open pop-up notes (tools, hackathons, media skills, education). Hover shows a tooltip on desktop; click or tap opens the note, and `Esc` closes it.
- **Progress navigation.** A side dot-nav jumps to each section, and a "Skip to contact" link jumps straight to the end.
- **Accessible and adaptive.**
  - Respects `prefers-reduced-motion`
  - Light and dark colour tokens through `prefers-color-scheme`
  - Safe-area insets for phones with notches
  - Responsive layout for mobile (cards dock to the bottom, FOV widens in portrait)
  - Graceful messages if WebGL or the CDN libraries fail to load

---

## The journey

| Scroll section | Room | Content |
|----------------|------|---------|
| 1 | Electronics lab | Research Intern at IIITDMJ Design Lab (multisensory anxiety-relief system: app, wearable, smart desk lamp); Documentation Lead for the IN-SPACe & ISRO CanSat Competition |
| 2 | App development room | GitHub projects: Meme Sharing Android App (Kotlin, REST API, caching and sharing) and a News App; hackathon notes |
| 3 | Creative studio | Digital & Cinematics Head at AITRONICS hub, JIIT; creative volunteering; DaVinci Resolve, Procreate, AutoCAD |
| End | Landing | Contact links (email and LinkedIn) |

**Hotspot notes** (click the `+` markers in the 3D scene):

- **Electronics bench:** tools and simulation (PSPICE, Proteus, MATLAB, Arduino)
- **App development desk:** languages and hackathons
- **Creative corner:** design and media tools
- **Book:** education background

---

## Tech stack

| Purpose | Library / API |
|---------|---------------|
| 3D rendering | [Three.js r128](https://threejs.org/) |
| Scroll animation and UI transitions | [GSAP 3.12.5](https://gsap.com/) and ScrollTrigger |
| Textures | Canvas 2D (procedurally generated) |
| Fonts | [Anton](https://fonts.google.com/specimen/Anton), [Caveat](https://fonts.google.com/specimen/Caveat), [Patrick Hand](https://fonts.google.com/specimen/Patrick+Hand) via Google Fonts |
| Everything else | Vanilla HTML, CSS, and JavaScript |

Libraries load from cdnjs, so an internet connection is needed on first load.



## How it works

1. **Scene.** Three rooms are laid out along the negative Z axis and joined by corridors. Helper functions (`B` for boxes, `CY` for cylinders, `S2` for textured planes, `shell`, `door`, `desk`, `bench`, and others) keep the room-building code compact.
2. **Flight path.** A `CatmullRomCurve3` defines the airplane's route. The scroll position is remapped to a position on that curve with `mapU()`, which also adds short "pauses" at key desks.
3. **Scroll to animation.** GSAP ScrollTrigger tracks overall page progress. A ticker loop eases the current progress toward the target, moves the plane and camera, and shows the cards whose `data-a` and `data-b` attributes bracket the current progress.
4. **Interaction.** A Three.js `Raycaster` detects hover and click on the hotspot sprites and opens the pop-up note.

---

## Project structure

```
.
├── index.html   # markup, styles, 3D scene, and scroll logic
└── README.md
```

---

## Customising

- **Edit card content:** change the `<aside class="card paper">` blocks in the HTML. The `data-a` and `data-b` attributes set the scroll range (0 to 1) during which each card is visible.
- **Edit hotspot notes:** change the `INFO` object in the script.
- **Move or add hotspots:** edit the array of `[key, x, y, z]` entries right after `INFO`.
- **Change colours:** edit the CSS variables at the top (`--ink`, `--acc`, `--card`) and the colour constants in the scene (`WC`, `FL`, `CE`, `WOOD`, and so on).
- **Change the flight path:** edit the control points passed to `CatmullRomCurve3`, then update the `SK` / `UK` arrays so scroll timing still matches the rooms.
- **Update contact links:** edit the `mailto:` and LinkedIn links in the nav and the `#end` card.

---

## Browser support

Current versions of Chrome, Edge, Firefox, and Safari with WebGL enabled. On devices without WebGL, the page shows a friendly fallback message.

---

## Related projects

- [The-desklamp](https://github.com/mohnanidisha/The-desklamp): interactive simulation of the multisensory smart desk lamp
- [meme-sharing-app](https://github.com/mohnanidisha/meme-sharing-app): Android app in Kotlin
- [news-app](https://github.com/mohnanidisha/news-app)
- [All repositories](https://github.com/mohnanidisha?tab=repositories)

---

## Contact

**Disha Mohnani**
- Email: [dishamohnani20@gmail.com](mailto:dishamohnani20@gmail.com)
- LinkedIn: [linkedin.com/in/dishamohnani](https://www.linkedin.com/in/dishamohnani)

---

## License

Add your preferred license (for example MIT) and include a `LICENSE` file. If you reuse the code, please credit the original author.
