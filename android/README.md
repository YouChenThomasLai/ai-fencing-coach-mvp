# Native Android app

The Android app is the main version of AI Fencing Coach. It uses Kotlin, Jetpack Compose, CameraX, MediaPipe Tasks, ONNX Runtime, and Room. Open this `android/` directory as a project in Android Studio.

## Features

| Area | Current implementation |
| --- | --- |
| Realtime | Back camera preview, skeleton overlay, target tracking, action recognition, ranked coaching cues, and Android text to speech |
| Pose and action models | Selectable MediaPipe or YOLO pose backend, plus FenceNet ONNX inference |
| Postgame | Analyze selected videos on the device, review the report, and export annotated video |
| History | Save practice sessions locally with Room and review session details |
| Settings | Training mode, pose backend, target side, voice, feedback focus, and summary provider |
| Summaries | Offline playbook, with optional Gemini or OpenAI summaries |

The live pipeline is CameraX → pose estimation → target tracking → normalization and FenceNet → heuristic checks → overlay and voice feedback. Core analysis does not require a Python server. The app uses portrait orientation and the back camera by default.

The main UI is in `app/src/main/java/com/aifencingcoach/MainActivity.kt`; the pipeline and storage modules are under `app/src/main/java/com/aifencingcoach/runtime/`.

## Run

1. Open `android/` in Android Studio and install the SDK or Gradle components it requests.
2. Confirm that `app/src/main/assets/` contains `fencenet_v2.onnx`, `yolo_pose.onnx`, `pose_landmarker_lite.task`, and the two playbook JSON files. They are included in this repository.
3. Connect an Android phone with USB debugging enabled and run the `app` configuration. Use a physical device to evaluate camera latency and voice output.

To regenerate the ONNX assets from Python weights, run these commands from the **repository root**:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe scripts/export_fencenet_onnx.py
.\.venv\Scripts\python.exe scripts/export_yolo_pose_onnx.py
```

See the [asset notes](app/src/main/assets/README.md) for the MediaPipe model download URL.

## Test

From `android/`, run `./gradlew testDebugUnitTest` (`.\gradlew.bat testDebugUnitTest` on Windows). Camera, audio, and latency still need device testing.
