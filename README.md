# PROJECT LEARN IO (PREC)

LEARNIO lets kids learn English letters by tracing them in the air in front of a webcam. A live hand-tracking model follows their fingertip, draws the trail on screen, and matches the shape to a letter in real time — no pen, paper, or app install required.

Everything runs **entirely in the browser**. No video is ever recorded, uploaded, or stored anywhere.

## How it works

1. The browser turns on the webcam (`getUserMedia`) — a live stream, nothing saved.
2. [MediaPipe HandLandmarker](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) finds 21 hand landmarks per frame, on-device.
3. The index fingertip's position is tracked every frame while the finger is extended, building a live stroke.
4. When the hand pauses or lowers (or you click **Check my letter**), the stroke is compared against letter templates using the [$1 Unistroke Recognizer](https://dl.acm.org/doi/10.1145/1294211.1294238) algorithm.
5. The matched letter is shown instantly, with a star for a correct match.

## Supported letters

`C  O  L  S  U  V  W  Z  N  M`

These are all letters that can be drawn in one continuous stroke without lifting your hand — a good fit for the recognition algorithm used here. Multi-stroke letters (A, B, E, F, ...) aren't supported yet — see [Roadmap](#roadmap).

## Running it

No build step, no server, no dependencies to install.

1. Clone or download this repo.
2. Open `index.html` in any modern browser (Chrome, Edge, or Firefox recommended).
3. Click **Start camera** and allow camera access.
4. Hold up one finger and trace the letter shown on screen.

> **Note:** if the camera doesn't start when opening the file directly, serve it locally instead:
> ```bash
> python3 -m http.server 8000
> ```
> then visit `http://localhost:8000`.

### Hosting it online

This is a static site — it can be deployed as-is to GitHub Pages, Netlify, Vercel, or any static host. Camera access requires **HTTPS** (or `localhost`) once it's not a local file, and all of the hosts above provide that automatically.

## Tech stack

- Plain HTML / CSS / JavaScript — no framework, no build tools
- [MediaPipe Tasks Vision](https://www.npmjs.com/package/@mediapipe/tasks-vision) (loaded from a CDN) for real-time hand tracking
- A custom implementation of the [$1 Unistroke Recognizer](https://dl.acm.org/doi/10.1145/1294211.1294238) for shape-to-letter matching

## Project structure

```
air-abc/
├── index.html     # the entire app: markup, styles, and logic
├── LICENSE
└── README.md
```

## Roadmap

- [ ] Support multi-stroke letters (A, B, D, E, F, ...) via pause-based stroke segmentation
- [ ] Train a small on-device ML classifier (TensorFlow.js) for higher accuracy
- [ ] Add sound effects and a mascot for extra engagement
- [ ] Add lowercase letters and numbers
- [ ] Save progress across sessions (locally, per device)

## License

MIT — see [LICENSE](LICENSE).
