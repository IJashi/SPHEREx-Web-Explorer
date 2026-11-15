# How to Run

## Requirements

- **Python 3.11 or 3.12.** Python 3.13 and newer, and 3.10 and older, are not supported.
- An internet connection. The app downloads its data live from NASA's IRSA archive.

All commands below are run from the project folder (the folder that contains
`backend/`, `frontend/` and this file).

## 1. Create a virtual environment

Windows (PowerShell):
```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

macOS / Linux:
```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

> If PowerShell blocks `Activate.ps1`, run
> `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` once, or skip activation
> and call `.\.venv\Scripts\python.exe` directly.

## 2. Install the libraries

```bash
python -m pip install -r backend/requirements.txt
```

To also run the tests, install the dev requirements instead:
```bash
python -m pip install -r backend/requirements-dev.txt
```

## 3. Start the server

```bash
cd backend
uvicorn app.main:app --port 8000
```

Open **http://localhost:8000/** in your browser. Press `Ctrl+C` in the terminal to stop the server.

## Running from PyCharm

1. **File → Open** the project folder itself (not its parent folder).
2. **Settings → Project → Python Interpreter → Add Interpreter → Add Local Interpreter → Existing**,
   then select `.venv\Scripts\python.exe`.
3. Optional: **Settings → Tools → Python Integrated Tools → Package requirements file** →
   `backend/requirements.txt`, so PyCharm's "Install requirements" prompt works.
4. **Run → Edit Configurations → + → Python**, then set:
   - **Module name:** `uvicorn`
   - **Parameters:** `app.main:app --port 8000`
   - **Working directory:** the project's `backend` folder
   - **Interpreter:** the `.venv` interpreter
5. Click **Run** and open http://localhost:8000/.

## Running with Docker (alternative)

If you have Docker installed, you don't need Python or a virtual environment:
```bash
docker compose up --build
```
Then open http://localhost:8000/.

## Command-line version (no browser)

With the virtual environment active:
```bash
python cli/spherex_blink.py "Barnard's star" --fov 3 --detectors D6 -o ./out
```
This saves `frames.npz` and `metadata.json` into `./out`.

## Running the tests

```bash
cd backend
python -m pytest
```
By default this skips the tests that contact the IRSA and SIMBAD services over the internet.
To run those as well: `python -m pytest -m live`.
