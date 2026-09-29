# AI Fencing Coach

這個專案從 Python 桌面／Web 原型，發展到目前的 **原生 Android 版本**。主要成品在 [`android/`](android/README.md)；Python 原型仍保留供模型匯出、分析與除錯使用。

## 目前的版本

| 位置 | 用途 | 狀態 |
| --- | --- | --- |
| [`android/`](android/README.md) | Kotlin + Jetpack Compose 手機 App | 主要版本；即時教練、影片分析、歷史紀錄 |
| [`web/`](web/README.md) | Python Web／桌面原型 | 可獨立啟動，用於片段分析、即時串流與啟發式規則除錯 |
| `src/`、`inference/` | Python 姿態、模型、追蹤與回饋流程 | Web 原型及模型匯出共用 |
| `scripts/`、`weights/` | 資料準備、ONNX 匯出、訓練權重 | Android 資產重建用；權重請保留 |
| [`docs/`](docs/README.md) | 開發、研究與論文資料 | 部分早期文件描述舊版原型 |

## Android 最終版本做了什麼

- 手機端 CameraX 即時畫面，MediaPipe 或 YOLO 姿態偵測，鎖定目標選手。
- FenceNet ONNX 動作辨識、規則式姿勢檢查、回饋排序、骨架疊圖及語音提示。
- 選取影片進行 Postgame 分析，產出報告並可匯出標註影片。
- Room 儲存練習紀錄與歷史；可使用離線 playbook 摘要，或選用 Gemini／OpenAI 摘要。
- 不需 Python 伺服器即可執行核心分析。詳細功能與安裝方式見 [Android README](android/README.md)。

## 開發脈絡

1. Python 原型：YOLO 姿態、FenceNet、啟發式回饋、Gradio 片段分析與即時 Web／桌面展示。
2. 原生 Android：移植模型推論與回饋流程，加入即時鏡頭、影片分析、語音及手機介面。
3. 後續 Android 完善：歷史紀錄、雙語 playbook、AI 摘要選項、影片匯出及介面調整。

Web 原型的啟動方式在 [web/README.md](web/README.md)。研究與論文資料保留在 `docs/research/` 與 `docs/paper/`。

## 注意

- 從專案根目錄執行 Python 指令；`web/` 的入口使用 `python -m web.<module>`。
- Android 可直接使用已附的 `android/app/src/main/assets/` 模型。若要重新匯出，請依 [Android README](android/README.md) 執行。
- `fencing_coach.db` 是 Python 原型的 SQLite 資料，整理時保留，避免遺失既有紀錄。
- `docs/dev/archive/` 是早期設計與除錯筆記；實際 Android 行為以目前程式碼為準。
