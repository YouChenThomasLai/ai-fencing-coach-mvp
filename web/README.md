# Python Web and desktop prototype

These tools predate the native Android app and remain useful for clip analysis, live demos, and debugging. Run every command from the **repository root**.

On Windows, create an environment and install dependencies:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Use `.\.venv\Scripts\python.exe` in place of `python` in the commands below, or activate the environment first.

| Command | Purpose |
| --- | --- |
| `python -m web.app` | Gradio clip analysis, annotations, summaries, and session history; default port 7860 |
| `python -m web.web_realtime` | Browser live stream and heuristic debug panel; default port 8000 |
| `python -m web.heuristic_visualizer` | Frame by frame heuristic inspection of a clip; default port 7862 |
| `python -m web.realtime_heuristic_visualizer --source 0` | Local OpenCV live heuristic debugging |
| `python -m src.realtime.realtime_app --source 0` | Local webcam coaching with spoken cues |

The tools share the root `inference/`, `src/`, and `coach_playbook.json`. `web/database.py` stores sessions in the root `fencing_coach.db`; `web/llm_agent.py` can optionally use `GEMINI_API_KEY` from a root `.env` file. Without that key, clip summaries use the playbook. Generated videos and logs go under the ignored `web_outputs/` directory.

For Python feedback changes, see [Adding or Tuning Heuristics](../docs/dev/ADDING_HEURISTIC.md). Model preparation and export scripts are in the root `scripts/` directory.
