# ✋ Hand Painter

A browser-based painting app that uses your webcam and hand gestures to draw — no mouse, no touch, just your hands.

Built with [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) and the Canvas API. Runs entirely in the browser as a single HTML file — no install, no server, no dependencies to manage.

---

## Demo

Open `hand-painter.html` in Chrome, allow camera access, and start painting.

---

## Gestures

| Gesture | Action |
|---|---|
| ☝️ Any extended finger | Draws on the canvas — tracks whichever fingertip is highest |
| 🤏 Pinch (thumb + index, spread/close) | Resizes the brush — spread apart to go bigger, pinch together to go smaller |
| 🤙 Pinky finger only up | Hold briefly to clear the canvas — a red pulse ring appears as confirmation |

---

## Features

- **Any finger draws** — index, middle, ring, or pinky; whichever is most extended becomes the brush tip
- **Live brush size preview** — a circle appears between your pinched fingers showing the current size
- **Pinky-to-clear** — deliberate gesture (requires all other fingers curled) so it never fires accidentally
- **Colour palette** — 6 colours in the toolbar, click to switch
- **Camera overlay toggle** — show or hide the webcam feed underneath your strokes
- **Dark canvas** — black background, draws on top

---

## How to Run

1. Download `hand-painter.html`
2. Open it in **Chrome** or **Edge** (Firefox may have issues with MediaPipe's WASM)
3. Allow camera access when prompted
4. Start painting

No npm, no Python, no server. Just open the file.

---

## Controls

| Input | Action |
|---|---|
| Click colour dot | Switch brush colour |
| `cam off` button | Toggle webcam feed overlay |
| ☝ → extend finger | Start drawing |
| 🤏 → pinch | Resize brush |
| 🤙 → pinky only | Clear canvas |

---

## How It Works

MediaPipe Hands detects 21 landmarks on your hand in real time. Each frame:

1. **Which finger is drawing?** — checks all four fingertips, picks the one furthest above its knuckle joint
2. **Pinch detection** — measures distance between thumb tip and index tip relative to hand size
3. **Pinky-only detection** — requires index, middle, and ring to be curled while pinky is extended
4. **Drawing** — strokes are painted onto a persistent `<canvas>` layer; the overlay (hand skeleton + cursor) is on a separate canvas that clears every frame
5. **Mirror correction** — the overlay canvas is CSS-mirrored (`scaleX(-1)`) to match the flipped webcam feed; drawing coordinates are un-mirrored before being written to the paint canvas

---

## Tech Stack

| | |
|---|---|
| Hand tracking | [MediaPipe Hands JS](https://cdn.jsdelivr.net/npm/@mediapipe/hands/) |
| Camera | [MediaPipe Camera Utils](https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/) |
| Rendering | HTML5 Canvas API |
| Styling | Plain CSS (DM Mono font) |
| Framework | None — vanilla JS, single HTML file |

---

## Browser Support

| Browser | Status |
|---|---|
| Chrome | ✅ Fully supported |
| Edge | ✅ Fully supported |
| Firefox | ⚠️ May have issues with MediaPipe WASM |
| Safari | ⚠️ Not tested |

---

## Limitations

- Single hand only — MediaPipe is set to `maxNumHands: 1`
- Requires good lighting for reliable tracking
- Works best when hand is clearly visible against a non-cluttered background
- Painting is not saved — refreshing the page clears the canvas

---

## License

MIT
