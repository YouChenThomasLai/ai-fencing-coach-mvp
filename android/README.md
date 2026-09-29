# Android 原生版

這是目前主要的 App：Kotlin、Jetpack Compose、CameraX 與手機端模型推論。開啟 Android Studio 時選擇本 `android/` 資料夾；入口是 `app/src/main/java/com/aifencingcoach/MainActivity.kt`。

## 已完成的功能

下表的 `runtime/` 路徑均位於 `app/src/main/java/com/aifencingcoach/`。

| 功能 | 實作位置 |
| --- | --- |
| 首頁、Realtime、Postgame、設定 | `app/src/main/java/com/aifencingcoach/MainActivity.kt` |
| 即時鏡頭、姿態與骨架疊圖 | `runtime/PoseBackend.kt`、`runtime/LiveCoachPipeline.kt` |
| MediaPipe／YOLO 姿態切換、目標追蹤 | `runtime/PoseBackend.kt`、`runtime/TargetTracker.kt` |
| FenceNet ONNX、動作與姿勢判斷 | `runtime/FenceNetClassifier.kt`、`runtime/HeuristicsEngine.kt` |
| 回饋排序、語音提示、練習報告 | `runtime/FeedbackScheduler.kt`、`runtime/PracticeReportBuilder.kt` |
| 影片分析、標註影片匯出 | `runtime/PostgameVideoAnalyzer.kt`、`runtime/VideoAnnotator.kt` |
| 本機練習歷史與詳情 | `runtime/database/`、`HistoryScreen.kt`、`SessionDetailScreen.kt` |
| 離線 playbook、選用 Gemini／OpenAI 摘要 | `runtime/PlaybookRepository.kt`、`runtime/GeminiAgent.kt` |

即時流程：CameraX → 姿態模型 → 目標鎖定 → 正規化與 FenceNet → 啟發式規則 → 畫面與語音回饋。Postgame 使用同一套手機端分析概念處理使用者選取的影片。核心流程不需要後端；AI 摘要是可選功能。

App 使用直向畫面；預設後鏡頭。設定中可調整練習模式、姿態模型、目標側、語音、回饋項目和摘要方式。

## 開啟與執行

1. 用 Android Studio 開啟 `android/`，安裝它提示的 SDK／Gradle 元件。
2. 確認 `app/src/main/assets/` 有 `fencenet_v2.onnx`、`yolo_pose.onnx`、`pose_landmarker_lite.task` 和中英文 playbook；目前專案已附這些檔案。
3. 連接開啟 USB 偵錯的 Android 手機，執行 `app`。相機延遲請以實機測試。

若要從 Python 權重重建 ONNX 資產，從**專案根目錄**執行：

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python scripts/export_fencenet_onnx.py
python scripts/export_yolo_pose_onnx.py
```

若需重抓 MediaPipe 模型，下載位置與檔名見 [`app/src/main/assets/README.md`](app/src/main/assets/README.md)。

## 驗證

在 `android/` 內執行 `./gradlew testDebugUnitTest`（Windows：`.\gradlew.bat testDebugUnitTest`）。這會執行 `app/src/test/` 的單元測試；鏡頭、語音與效能仍需實機驗證。
