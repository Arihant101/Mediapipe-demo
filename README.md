# Body Controller Demos

Live MediaPipe demos that run entirely in your browser. No install, and no video leaves your device.

| Demo | What it does | Jump straight to it |
|---|---|---|
| **Fingers** | Counts raised fingers on one or two hands, thumbs included (up to 10) | `#fingers` |
| **Face** | Sunglasses, devil horns, crown, mustache or clown nose, plus a mood detector (smile, frown, surprise, blink, wink, mouth open) | `#face-glasses` `#face-horns` `#face-crown` `#face-mustache` `#face-nose` `#face-none` |
| **Full body** | Erases a person and turns them into an otter, robot, X-ray skeleton, neon light trails or an anime girl | `#body-otter` `#body-robot` `#body-skeleton` `#body-neon` `#body-anime` |

**Live site:** [https://arihant101.github.io/mediapipe-demo/](https://arihant101.github.io/Mediapipe-demo/)

## Run it

- **Easiest:** open the live site link above.
- **Locally:** double-click `index.html` and open it in Chrome or Edge. No server needed.
- **From a notebook:** open `run_demos.ipynb` in Google Colab (File → Upload notebook) or Jupyter. It shows three ways to launch the page, plus the finger counter and mood detector in Python.

### Put it on GitHub Pages

1. Upload `index.html` (and the rest of this folder) to a public repo.
2. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, pick `main` and `/ (root)`, then **Save**.
3. After a minute the site is live at `https://<username>.github.io/<repo>/`.

## Using it

- Press **Start camera** and allow access.
- Switch demos with the tabs or keys **1**, **2**, **3**. Press **O** to cycle face filters or body characters.
- **External camera:** plug in a USB webcam (before or after starting) and pick it from the **Camera** list. The page remembers your choice. Untick **Mirror** if the camera faces the room rather than you.
- **Full body:** stand back so the whole body fits. Have the person step out, press **Capture empty background**, then they walk back in. If the camera moves or the light changes, the page asks you to capture again.
- **Snapshot** saves a PNG of the current frame.

### OBSBOT webcams

The page recognizes OBSBOT cameras by name, shows the model in the status bar, and adds a control panel:

- **Zoom slider and Re-center camera**, when Chrome exposes them. If they don’t appear, press **Enable zoom and gimbal controls**, and Chrome asks for permission to move the camera.
- **Full body zooms out automatically** so the whole body fits.
- The camera always runs at 1280×720, 30 fps, which keeps tracking fast even though the OBSBOT can do 4K.
- **Turn off AI tracking before capturing the background.** The full-body trick needs a still camera.
- The OBSBOT reacts to some hand gestures itself, which can move or zoom it during the Fingers demo. If your model allows it, turn gesture control off in OBSBOT Center.

## How it works

All demos use [MediaPipe Tasks Vision](https://ai.google.dev/edge/mediapipe/solutions/guide) 1.0.1, loaded from jsDelivr. All three models load in the background, so switching tabs is instant.

- **Fingers:** Hand Landmarker gives 21 points per hand. A finger is up when its tip is farther from the wrist than its middle joint. The thumb is measured from the pinky base instead, because it folds sideways. The count only changes once it’s steady for a few frames, so it doesn’t flicker.
- **Face:** Face Landmarker gives 478 points and 52 expression scores. Each filter is pinned to a few points (eye corners, forehead, nose tip) and scaled and rotated with the face. The mood detector combines expression scores like `mouthSmileLeft`, `browDownLeft` and `jawOpen`.
- **Full body:** Pose Landmarker gives 33 body points and a mask of the person. The mask is filled with the saved background, then a character is drawn on the joints.

To make your own, edit `countHand()`, `readMood()`, or one of the drawing functions such as `drawHorns()`, `drawCrown()`, `drawOtter()`, `drawRobot()` or `drawAnime()`.

Made by ml@psu.
