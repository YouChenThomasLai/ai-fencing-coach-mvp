# Python Web／桌面原型

這裡收納 Android 版之前的 Python 介面。所有指令都從**專案根目錄**執行，依賴安裝於根目錄的 `requirements.txt`。

在 Windows 建立環境：

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

下表的 `python` 可換成 `.\.venv\Scripts\python.exe`。

| 入口 | 用途 | 指令 |
| --- | --- | --- |
| `app.py` | Gradio 影片片段分析與歷史 | `python -m web.app` |
| `web_realtime.py` | 瀏覽器即時畫面與回饋 | `python -m web.web_realtime` |
| `heuristic_visualizer.py` | 影片姿勢規則除錯 | `python -m web.heuristic_visualizer` |
| `realtime_heuristic_visualizer.py` | 本機 OpenCV 即時除錯 | `python -m web.realtime_heuristic_visualizer --source 0` |

`database.py` 和 `llm_agent.py` 是此原型的資料庫與摘要模組。共用推論程式仍在根目錄的 `inference/` 與 `src/`，設定用 playbook 在根目錄的 `coach_playbook.json`。生成的影片與紀錄會放到根目錄的 `web_outputs/`；Python 原型的 SQLite 檔案是根目錄的 `fencing_coach.db`。

更多舊版使用說明見 [`docs/dev/QUICKSTART.md`](../docs/dev/QUICKSTART.md)。
