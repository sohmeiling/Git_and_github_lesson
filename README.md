# Git & GitHub Lesson Notes

This guide walks through the steps for setting up Git and GitHub, preparing VS Code, and working with repositories.  
It is written for **Windows users with VS Code**, but Mac notes are included where relevant.  

---

## Step 0 — Shortcuts and Useful Info
- **Windows:**  
  - `Ctrl + C` → Copy  
  - `Ctrl + V` → Paste  
- **Mac:**  
  - `Cmd + C` → Copy  
  - `Cmd + V` → Paste  

Show hidden folders:  
- Windows: File Explorer → View → tick *Hidden items*  
- Mac: Finder → `Cmd + Shift + .`

---

## Step 1 — Install Git
Check if Git is installed:
```bash
git --version
```

If not:
- Download from git-scm.com.
- Windows: Run installer (keep defaults).
- Mac: Often preinstalled. If not, install via Homebrew:

```bash
brew install git
```

Verify:
```bash
git --version
```

Reference: [Pro Git Book, Chapter 1.5: Getting Started — Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

---

## Step 2 — Configure Git (First Time Only)
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Check settings:
```bash
git config --list
```

These values are stored in the global config file (~/.gitconfig).

Reference: [Pro Git Book, Chapter 1.6: First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

---

## Step 3 — Generate SSH Keys
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```


- Press Enter for default file location.

- Press Enter twice for no passphrase.

Key locations:

- Windows: C:\Users\<username>\.ssh\

- Mac: /Users/<username>/.ssh/

Copy public key:

Windows:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub
```

Mac:
```bash
cat ~/.ssh/id_ed25519.pub
```

Add to GitHub → Settings → SSH and GPG keys → New SSH Key.

Reference: [GitHub Docs — Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

---

## Step 4 — Prepare VS Code for Git/GitHub

1. Install VS Code: https://code.visualstudio.com/

2. Install extensions (Extensions tab):

- GitHub Pull Requests and Issues

- GitLens (optional, for commit history)

3. Open terminal inside VS Code:

- Windows: `Ctrl + ``

- Mac: `Cmd + ``

- Or: View → Terminal

4. Terminal type:

- Windows: PowerShell or Git Bash

- Mac: zsh/bash

---

## Step 5 — Create New Repository on GitHub

1. Log in to GitHub.

2. Click New → Repository.

3. Tick Initialise with README file → Create.

4. Copy the repo’s SSH URL (not HTTPS, since we set up SSH).

---

## Step 6 — Clone Repo in VS Code

### Option A (GUI):

- Open Command Palette (Ctrl+Shift+P / Cmd+Shift+P).

- Type Git: Clone → paste SSH URL → choose folder → Open repo.


### Option B (Terminal):

```bash
cd Desktop
git clone git@github.com:<owner>/<repo>.git
cd <repo>
```

---

## Step 7 — Stage, Commit, and Push (VS Code GUI)

**Add files:**

- Create LICENSE file.

- Edit README.md.

- Create pingpong.py.

**Stage changes:**

- Source Control tab → hover file → +.

- Files move to Staged Changes.

**Commit:**

- Write message:

```sql
add license, update readme, create pingpong.py
```

- Press Ctrl+Enter (Win) / Cmd+Enter (Mac) or click ✓.

Push:

- Click Sync Changes (🔄) or Push.

- Refresh repo on GitHub to see files.

Plain words:

- Stage = choose files.

- Commit = snapshot.

- Push = upload to GitHub.

Reference: [Pro Git Book, Chapter 2.2: Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

---

## Step 9 — Stage, Commit, and Push (Terminal)

Check status:

```
git status
```

Stage:
```
git add .
```

Commit:
```
git commit -m "add license, update readme, create pingpong.py"
```

Push:
```
git push -u origin main
```

---

## Step 10 — Branching Workflow

**Create branch (GUI):**

- Bottom-left → branch name → New Branch → e.g., feature-score-system.

**Create branch (terminal):**
```
git checkout -b feature-score-system
```

Make changes → commit → push:
```
git add .
git commit -m "add score variable"
git push -u origin feature-score-system
```

On GitHub: click Compare & pull request → Create PR.

Reference: [Pro Git Book, Chapter 3.2: Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

---

## Step 11 — Merging & Resolving Conflicts

**Merging with no conflicts:**

- On GitHub → Merge pull request → Confirm.

- Update local repo:
```
git checkout main
git pull origin main
```

**Conflict example in pingpong.py:**

```
<<<<<<< main
score = 0
=======
score = 100
>>>>>>> feature-score-system
```

**Resolve in VS Code:**

- Choose Accept Current / Incoming / Both or edit manually.

- Save → Stage → Commit → Push.

**Resolve in terminal:**

- Edit file manually (remove conflict markers).

- Stage & commit:
```
git add pingpong.py
git commit -m "resolve merge conflict"
git push
```

Reference: [Pro Git Book, Chapter 3.3: Branch Management](https://git-scm.com/book/en/v2/Git-Branching-Branch-Management)

---

## ✅ Summary

1. Setup Git + VS Code

2. Create repo on GitHub

3. Clone repo into VS Code

4. Stage → Commit → Push changes

5. Create & push branches

6. Open Pull Requests

7. Merge & resolve conflicts

This is the basic Git/GitHub workflow for coding projects.

---

## Additional Notes
**Working with Virtual Environments (for Python projects)**

### 1. Finding an existing virtual environment

Sometimes projects already include a virtual environment (e.g., .venv folder).

- **Windows:**
Look inside your project folder for a .venv or env folder.
```
dir .venv
```

- **Mac/Linux:**
```
ls -a
```

(check for .venv/ folder).

If no environment exists, create one:

# Windows
```
python -m venv .venv
```
# Mac
```
python3 -m venv .venv
```

---

### 2. Activating the virtual environment

**Windows (PowerShell):**
```
.venv\Scripts\Activate.ps1
```

**Windows (Git Bash):**
```
source .venv/Scripts/activate
```

**Mac/Linux:**
```
source .venv/bin/activate
```

When activated, you’ll see (.venv) at the start of your terminal prompt.

Deactivate with:
```
deactivate
```

---

### 3. Run and test if Pygame file works

Make sure pygame is installed inside the environment:
```
pip install pygame
```

Run your game (e.g., pingpong.py):
```
python pingpong.py     # Windows
python3 pingpong.py    # Mac/Linux
```

If it runs without errors → environment is correctly set.

References

[Python venv documentation](https://docs.python.org/3/library/venv.html)

[Pygame installation guide](https://www.pygame.org/wiki/GettingStarted)

---

## Selecting the Python Interpreter in VS Code

Even after activating, VS Code sometimes needs to be told which interpreter to use.

1. In VS Code → Command Palette (Ctrl+Shift+P on Windows / Cmd+Shift+P on Mac).

2. Search: Python: Select Interpreter.

3. Choose the interpreter inside your project’s .venv.

- On Windows: .\.venv\Scripts\python.exe

- On Mac/Linux: ./.venv/bin/python3

4. Status bar (bottom right of VS Code) should now show your virtual environment (e.g., .venv).

---

## Run and Test with Pygame

Install pygame inside the environment:
```
pip install pygame
```

Run the file in VS Code terminal:
```
python pingpong.py     # Windows
python3 pingpong.py    # Mac/Linux
```

If a game window opens → environment and interpreter are working.

