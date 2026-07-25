# Python .venv and Jupyter Kernel Cheat Sheet

This guide covers creating and activating a Python virtual environment, registering it as a Jupyter kernel, listing and locating kernels, and renaming the kernel for your project on macOS.

## Project Assumption

Project folder:

```bash
/Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI
```

Virtual environment:

```bash
.venv
```

---

## 1. Go to your project folder

```bash
cd "/Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI"
```

Verify the folder contents:

```bash
ls -la
```

You should see your virtual environment folder and project files.

---

## 2. Activate the virtual environment

```bash
source .venv/bin/activate
```

Your terminal prompt should change to include the virtual environment name:

```bash
(.venv) prasadimmadi@Mac Project_AgenticAI %
```

---

## 3. Verify Python is using the .venv

```bash
which python
```

Expected output:

```bash
/Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI/.venv/bin/python
```

Check the version:

```bash
python --version
```

---

## 4. Install or verify Jupyter kernel support

Inside the activated virtual environment:

```bash
pip install ipykernel
```

Verify installation:

```bash
pip show ipykernel
```

---

## 5. Register the .venv as a Jupyter kernel

Recommended command:

```bash
python -m ipykernel install \
  --user \
  --name project_agenticai_venv \
  --display-name "AgenticAI_Venv"
```

This creates a kernel entry that appears in VS Code and Jupyter.

---

## 6. List all available kernels

```bash
jupyter kernelspec list
```

Example output:

```bash
Available kernels:

project_agenticai_314
    /Users/prasadimmadi/Library/Jupyter/kernels/project_agenticai_314

project_agenticai_prasad
    /Users/prasadimmadi/Library/Jupyter/kernels/project_agenticai_prasad

project_agenticai_venv
    /Users/prasadimmadi/Library/Jupyter/kernels/project_agenticai_venv

python3
    /Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI/.venv/share/jupyter/kernels/python3
```

---

## 7. Find which kernel is using your .venv

From the kernel list, look for the one tied to your project environment, usually:

```bash
/Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI/.venv/share/jupyter/kernels/python3
```

That indicates the kernel is using your project’s .venv.

---

## 8. Locate kernel folders

### User-level kernels

```bash
ls ~/Library/Jupyter/kernels
```

### Project .venv kernels

```bash
ls ".venv/share/jupyter/kernels"
```

Example output:

```bash
python3
```

---

## 9. Inspect a kernel configuration

Go to the kernel directory:

```bash
cd ".venv/share/jupyter/kernels/python3"
```

View the configuration file:

```bash
cat kernel.json
```

Example content:

```json
{
  "argv": [
    "/Users/prasadimmadi/Desktop/Git Local/Project_AgenticAI/.venv/bin/python",
    "-m",
    "ipykernel_launcher",
    "-f",
    "{connection_file}"
  ],
  "display_name": "Python 3",
  "language": "python"
}
```

The `argv` path confirms which Python environment the kernel uses.

---

## 10. Rename a kernel manually

Your Jupyter version may not support the built-in rename command, so rename it manually.

### Step 1: Go to the kernels folder

```bash
cd ".venv/share/jupyter/kernels"
```

### Step 2: Rename the folder

Example:

```bash
mv python3 AgenticAI_Venv
```

### Step 3: Edit the kernel.json file

```bash
cd AgenticAI_Venv
nano kernel.json
```

Change:

```json
"display_name": "Python 3"
```

to:

```json
"display_name": "AgenticAI_Venv"
```

Save with:

```bash
Ctrl + O
Enter
Ctrl + X
```

---

## 11. Locate and remove old or duplicate kernels

### Step 1: List all installed kernels

```bash
jupyter kernelspec list
```

This shows the kernel names and their storage locations.

### Step 2: Locate the kernel folders manually

User-level kernels:

```bash
ls ~/Library/Jupyter/kernels
```

Project-level kernels inside your virtual environment:

```bash
ls ".venv/share/jupyter/kernels"
```

You can identify old or duplicate kernels by their folder names.

### Step 3: Remove a kernel

```bash
jupyter kernelspec uninstall kernel_name
```

Example:

```bash
jupyter kernelspec uninstall project_agenticai_prasad
```

If prompted, confirm with:

```bash
y
```

### Step 4: Remove the folder manually if needed

If the kernel still appears, delete its folder manually:

```bash
rm -rf ~/Library/Jupyter/kernels/kernel_name
```

Example:

```bash
rm -rf ~/Library/Jupyter/kernels/project_agenticai_prasad
```

### Step 5: Verify removal

```bash
jupyter kernelspec list
```

You should no longer see the removed kernel in the list.

---

## 12. Refresh VS Code kernel list

In VS Code:

```bash
Cmd + Shift + P
```

Search for:

```bash
Developer: Reload Window
```

Then open your notebook and choose the kernel named:

```bash
AgenticAI_Venv
```

---

## 13. Deactivate the virtual environment

When you are done:

```bash
deactivate
```

Your prompt should return to the normal shell prompt.

---

## Recommended setup for your AI project

For your project, it is best to keep only one clean kernel linked to your .venv, such as:

```bash
AgenticAI_Venv
```

and remove old duplicates to avoid confusion in VS Code.
