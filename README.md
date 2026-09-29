# AI Fencing Coach

AI Fencing Coach is a fencing practice prototype. The **native Android app** is the main product; the Python Web and desktop tools are retained for analysis, model export, and debugging.

## Repository layout

| Path | Purpose |
| --- | --- |
| [`android/`](android/README.md) | Native Kotlin and Jetpack Compose app |
| [`web/`](web/README.md) | Python clip analysis, browser streaming, and visualizers |
| `src/`, `inference/` | Python models, pose processing, tracking, and feedback logic |
| `scripts/`, `weights/` | Dataset preparation, ONNX export, and model weights |
| [`docs/`](docs/README.md) | Active development notes and the paper PDF |

## Android app

The app runs its core analysis on the device. It supports live camera coaching with MediaPipe or YOLO pose estimation, target tracking, FenceNet ONNX action recognition, posture checks, a feedback queue, skeleton overlays, and spoken cues. Postgame analysis processes selected videos and can export annotated video. Room stores practice history. Summaries use the offline playbook by default; Gemini and OpenAI are optional.

Open [`android/`](android/README.md) in Android Studio to build and run it. The required model assets are already bundled in `android/app/src/main/assets/`.

## Python prototype

From the repository root, install `requirements.txt` and run `python -m web.app` for clip analysis or `python -m web.web_realtime` for browser streaming. See the [Web README](web/README.md) for setup and the other entry points.

`fencing_coach.db` contains the Python prototype's SQLite data and is kept in the repository. Generated caches and build outputs are ignored.
