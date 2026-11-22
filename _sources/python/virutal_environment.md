# Setting up a virtual environment

Pick **one** of the three tools below.

| Tool | Project / docs |
| --- | --- |
| uv | [docs.astral.sh/uv](https://docs.astral.sh/uv/) ([GitHub](https://github.com/astral-sh/uv)) |
| conda (Miniforge) | [Miniforge](https://github.com/conda-forge/miniforge), [conda docs](https://docs.conda.io/) |
| venv | [Python docs: venv](https://docs.python.org/3/library/venv.html) |

## uv (recommended)

Install uv (once):

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Create and use an environment:

```bash
uv venv --python 3.12          # creates .venv (downloads Python if needed)
source .venv/bin/activate      # Windows: .venv\Scripts\activate
uv pip install pandas matplotlib jupyterlab
```

Project-style alternative (writes `pyproject.toml` and a lock file):

```bash
uv init
uv add pandas matplotlib
uv run python script.py        # no activation needed
```

## conda (Miniforge)

Install [Miniforge](https://github.com/conda-forge/miniforge) (uses conda-forge by default), then:

```bash
conda create -n myenv python=3.12
conda activate myenv
conda install pandas matplotlib      # or: pip install ...
```

Export / recreate:

```bash
conda env export --from-history > environment.yml
conda env create -f environment.yml
```

Leave the environment with `conda deactivate`.

## venv (built into Python)

Needs only Python 3 installed (on Debian/Ubuntu also `sudo apt install python3-venv`).

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install pandas matplotlib
```

Save / restore packages:

```bash
pip freeze > requirements.txt
pip install -r requirements.txt
```

Leave the environment with `deactivate`.

## Tips

- Add `.venv/` to `.gitignore`.
- In VS Code: `Cmd/Ctrl+Shift+P` → "Python: Select Interpreter" → choose the new environment.
- For Jupyter: `pip install ipykernel` (or `uv pip install ipykernel`) inside the environment.
