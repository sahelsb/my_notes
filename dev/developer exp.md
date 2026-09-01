

## Project structure root run

##### The problem
The `src/` folder held flat top-level modules (`api.py, service.py, db.py, …`) that **imported
each other by bare name** (`from service import ...`). **Those imports only resolve when that
exact directory is on Python's import path (sys.path).**
  - `uv run python src/mcp_service.py` worked — **running a script auto-adds the script's own folder (src/) to sys.path.**
  - `uvicorn api:app` did not work from root — the **api:app import string is resolved against
  the current working directory**, which is why it forced `cd src && uvicorn ....`

##### The Solution
Turned the project into a proper installable package
Use a `src/-layout package`, not flat modules. Code lives in `src/<pkgname>/`, imports are relative or package-qualified (`from .db import / from mypkg.db import`).

1. Move `src/*.py` + `static/ `into `src/integra/` (**a real package** with `__init__.py`).
2. Change all **internal imports to relative** (`from .service import ...`).
3. Added a build backend + package config + console entry points in `pyproject.toml`:

  ```python
  
  ## terminal commands your package provides
  ## the command integra-api runs the function run_api inside the module integra.cli
  [project.scripts]
  integra-api   = "integra.cli:run_api"
  integra-mcp   = "integra.mcp_service:main"
  integra-index = "integra.main:main"


## This tells uv/pip: "my project is a real package — here's the tool that knows how to package it.
  [build-system]
  requires = ["hatchling"]
  build-backend = "hatchling.build"


## where your code lives , This is a hatchling-specific setting that answers one question: "which folder is the actual package to install?"
  [tool.hatch.build.targets.wheel]
  packages = ["src/integra"]
  ```
  
- hatchling is a build backend — a small program that knows how to take your source files
  and turn them into an installable package (a wheel).
	  - Without this block, your project was just "a folder with a `pyproject.toml` listing
	  dependencies." uv installed the dependencies but never installed your code — that's
	  exactly why imports depended on the working directory.
	  - With this block, `uv sync` actually installs integra into the venv, so `import integra`
	  works from anywhere.

- command-line command
	- Format is always `command-name = "module.path:function_name"`. The `:` separates the module from the function to call.
	  When you `uv sync`, it generates a tiny executable named integra-api in `.venv/bin/ `that, when run, imports integra.cli and calls run_api(). That's why `uv run integra-api` works from any directory — it's a real installed command, not a script file you have to point at.

  4. `uv sync` installs integra into the venv (editable), so **it imports from any directory**.


##### Summary
`__init__.py` makes a directory an importable package. It's why `from harness.case import Case` resolves. Without it, harness is just a directory on disk.

  Root files don't need one because they're already top-level modules — the project directory
  itself is on sys.path, so import agent works directly. A file at root is a module; a folder
  needs the marker to become a package.
##### Attention
**Never patch `sys.path` at runtime to make imports work. If you're reaching for `sys.path.insert(...)` in the script, the real problem is that the project isn't packaged.**

```python
sys.path.insert(0, str(Path(__file__).parent / "src")) 
```

**Rule of thumb**: if running your app depends on which folder you're standing in, the project isn't packaged correctly yet.


---

####  RateLimit vs. Timeout in eval runs

**RateLimit (429)** — Azure OpenAI refused the request.
  - Cause: the deployment's tokens-per-minute quota was exceeded. Shared
    deployment, so someone else running at the same time can trigger it.
  - Not our code

**Timeout** — the case took too long.
  - `config.CASE_TIMEOUT_SECONDS = 300`, enforced by `asyncio.wait_for` in
    `harness/agent_system.py`.
  - Surfaces as `TimeoutError`, never as `RateLimit`.
  - Means the agent itself was slow/stuck, not that the API refused.


---

### json vs josnl


 1. `JSONL — records.jsonl` : JSON Lines
	 one complete JSON object per line, no wrapping array.

 ```json
  {"run_id": "20260811T0803Z", "system": "agent", "gt_id": "300",
  "predicted": {"Anlage": "Fassabf."}, "seconds": 18.2}
  {"run_id": "20260811T0803Z", "system": "agent", "gt_id": "301",
  "predicted": {"Anlage": "Fassabf."}, "seconds": 17.4}
 ```

2. `JSON — run.json`
	one object wrapping everything

```json
{
    "run_id": "20260811T0803Z",
    "system": "agent",
    "cases": 3,
    "records": [
      { "gt_id": "300", "predicted": { "Anlage": "Fassabf." },
   "seconds": 18.2 },
      { "gt_id": "301", "predicted": { "Anlage": "Fassabf." },
   "seconds": 17.4 },
      { "gt_id": "307", "predicted": { "Anlage": "Flaschenabf."
  }, "seconds": 19.1 }
    ]
  }
```

---
### how to let a process run when laptop is idle

Both are now in tmux, detached from your terminal. You can close Windows Terminal, and even exit Claude Code — neither is a
  parent of these processes any more.

  What's running

  ┌─────────┬──────────────────────────────┬──────────────────────────────────────┐
  │ session │             what             │                 log                  │
  ├─────────┼──────────────────────────────┼──────────────────────────────────────┤
  │ integra │ the MCP/API server on :20000 │ ~/workspace/mcp/integra/server.log   │
  ├─────────┼──────────────────────────────┼──────────────────────────────────────┤
  │ eval    │ the 304-case agent sweep     │ ~/workspace/awa/maisel_eval/eval.log │
  └─────────┴──────────────────────────────┴──────────────────────────────────────┘

  Started at 23:16, case 1 done. Expect 3.5–6 hours, so finished somewhere between 03:00 and 05:00.

  Note I had to restart your server — it was in your other terminal's foreground process group (Sl+), so it would have died with
  that window and every case would have failed. It's the same command, just re-parented under tmux.

  Checking on it

  tmux ls                          # both sessions alive?
  tail -f ~/workspace/awa/maisel_eval/eval.log
  wc -l < .eval/records/2026-08-31_23-16-37-agent.jsonl    # cases done so far
  tmux attach -t eval              # watch live; detach again with Ctrl-b then d

  Your shell aliases tmux to a plugin function that doesn't exist in non-interactive shells — from an interactive prompt it's
  fine, but if you ever hit _zsh_tmux_plugin_run: command not found, use /bin/tmux.

  To stop it: kill -INT $(pgrep -f 'bin/maisel-eval') — use SIGINT, not kill -9. See below for why.

  One thing to fix before you sleep

  Your powercfg commands set the AC timeouts only. If the laptop is on battery, the -dc timeouts still apply and it will
  suspend. Either keep it plugged in, or run:

  powershell.exe -Command "powercfg /change standby-timeout-dc 0"
  powershell.exe -Command "powercfg /change hibernate-timeout-dc 0"

  Monitor timeout is harmless — the screen going dark doesn't suspend anything.

  Something the interruption taught us

  When I killed the earlier run with SIGKILL, it skipped finally: reset_environment(c) and left article 323 deleted from the 
  catalogue. That's not a crash — it's silent corruption: 323 would have been missing as a reference candidate for all 304
  cases, quietly lowering every score.

  I restored it from .eval/stammdaten.original.db and verified the catalogue is whole (314 reference articles, nothing missing).
  But it's a real fragility in the harness worth hardening later — a --verify that compares live against the original before a
  sweep starts would have caught it in a second.

  Seven leftover IN_REVIEW drafts are also lying around. They're excluded from reference search, so harmless; I didn't delete
  them.

  In the morning

  uv run maisel-grade --system agent     # pass@1 headline
  uv run python -m evaluation.funnel     # retrieval / selection / transcription split

  The funnel is the one to look at. The question it answers: of the +28.4 points now sitting inside the window, how many did the
  agent actually take? "Lost in selection" is the number that should have dropped.

---
 
 ### Runs
┌───────────────────┬──────────────────────────────────────┬──────────────────────────────────────┐
  │                   │              old (k=5)               │              new (k=15)              │
  ├───────────────────┼──────────────────────────────────────┼──────────────────────────────────────┤
  │ generation run_id │ 20260828T102003Z                     │ 20260831T211637Z                     │
  ├───────────────────┼──────────────────────────────────────┼──────────────────────────────────────┤
  │ grading run       │ .eval/runs/b0b5ef665790              │ .eval/runs/4009b3b31522              │
  ├───────────────────┼──────────────────────────────────────┼──────────────────────────────────────┤
  │ report            │ .eval/reports/b0b5ef665790/report.md │ .eval/reports/4009b3b31522/report.md 


----
