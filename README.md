# Project_AgenticAI

This repository contains Python notebooks that run with the standard Python 3 kernel.

## Local setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## VS Code

The workspace is configured to use `.venv/bin/python` as the default interpreter. After creating the virtual environment, reload VS Code and select the `Python 3` kernel in each notebook if prompted.

## Notes

- The notebooks use only the Python standard library.
- One notebook includes `input()` cells, so run it interactively from top to bottom.
