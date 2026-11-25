<div align="center">

  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" alt="Git logo" width="100" />

  # Git Tutorial

  **A hands-on repository for learning Git version control through practical file changes and data-ingestion scenarios.**

  <p>
    <a href="https://git-scm.com/doc"><img src="https://img.shields.io/badge/Git-Documentation-F05032?logo=git&logoColor=white" alt="Git Documentation"></a>
    <a href="https://github.com/shubhamthakur9771/Git_Tutorial"><img src="https://img.shields.io/badge/GitHub-Repository-181717?logo=github&logoColor=white" alt="GitHub Repository"></a>
    <img src="https://img.shields.io/badge/Status-Learning%20Project-blue" alt="Learning Project">
  </p>

  <p>
    <a href="#-overview">Overview</a> •
    <a href="#-repository-structure">Structure</a> •
    <a href="#-what-this-project-covers">Topics</a> •
    <a href="#-git-command-reference">Commands</a> •
    <a href="#-getting-started">Getting Started</a>
  </p>

</div>

---

## 📌 Overview

**Git Tutorial** is a practical learning repository for understanding how Git tracks changes and how a developer can manage files during an ongoing project.

The repository uses small text files that represent data-ingestion activities. These files provide a simple environment for practicing everyday version-control workflows: editing files, tracking changes, preparing commits, and understanding how multiple updates can affect the same working tree.

Rather than being a production data-ingestion application, this repository is focused on **learning Git through hands-on examples**.

### 🎯 Learning objectives

- Understand the Git repository and working-tree lifecycle.
- Track new and modified files.
- Stage selected changes before committing.
- Understand commits and project history.
- Practice working with multiple project files.
- Learn how `.gitignore` prevents selected files and directories from being tracked.
- Become familiar with branch-based collaboration and merge-conflict resolution through Git's command-line workflow.

## 🗂️ Repository structure

```text
Git_Tutorial/
│
├── README.md
├── .gitignore
│
├── data_ingest.txt
├── data_ingestion.txt
├── iot_data_ingestion.txt
│
└── silver/
    └── .gitkeep
```

### Files and directories

| Path | Purpose |
|---|---|
| `data_ingest.txt` | Text-based example of data-ingestion updates, including batch-ingestion notes and a bug-fix marker. |
| `data_ingestion.txt` | Example file containing successive edits, bug-fix notes, and big-data ingestion notes. |
| `iot_data_ingestion.txt` | Example of real-time/IoT data-ingestion updates. |
| `silver/` | A placeholder directory for the Silver layer. `.gitkeep` keeps the otherwise-empty directory in Git. |
| `.gitignore` | Lists local or generated paths that should not be tracked by Git. |
| `README.md` | Project documentation and Git command reference. |

## 📚 What this project covers

### 1. Repository and working-tree basics

A Git repository stores the project's tracked history. The working tree is where files are created and edited.

The usual lifecycle is:

```text
Working Directory → Staging Area → Local Repository → Remote Repository
```

- **Working directory:** Create or modify project files.
- **Staging area:** Select the changes that should go into the next commit.
- **Local repository:** Save a snapshot with a commit.
- **Remote repository:** Share commits with a hosted repository such as GitHub.

### 2. Tracking file changes

The text files in this repository are useful for observing how Git detects edits to existing files and additions of new files.

Useful commands:

```bash
git status
git diff
git diff --staged
git add data_ingest.txt
git add .
```

- `git status` shows the current branch and the state of files.
- `git diff` displays unstaged changes.
- `git diff --staged` displays changes already staged.
- `git add <file>` stages a selected file.
- `git add .` stages changes under the current directory.

### 3. Creating commits

A commit records the staged changes in the local repository.

```bash
git add .
git commit -m "Add data ingestion examples"
git log --oneline
```

A useful commit message briefly describes the change. Prefer focused commits that represent one logical update.

### 4. Understanding `.gitignore`

The repository's `.gitignore` contains:

```gitignore
.env
api_secrets.txt
bronze/
```

These patterns tell Git to ignore matching untracked paths:

| Pattern | Purpose |
|---|---|
| `.env` | Ignore a local environment configuration file. |
| `api_secrets.txt` | Ignore the named local text file. |
| `bronze/` | Ignore the `bronze` directory and its contents. |

**Important:** `.gitignore` does not automatically untrack files that Git already tracks. If a matching file was committed earlier, remove it from the index while keeping the local file:

```bash
git rm --cached <file>
git commit -m "Stop tracking ignored file"
```

Never commit real credentials, tokens, passwords, or private connection strings.

### 5. Branches and parallel development

Branches allow work to happen independently before changes are integrated.

Common commands:

```bash
git branch
git branch feature/data-ingestion
git switch feature/data-ingestion
```

To create and switch to a new branch in one command:

```bash
git switch -c feature/data-ingestion
```

After completing the work, stage and commit it:

```bash
git add .
git commit -m "Update data ingestion examples"
```

### 6. Merging changes

A merge integrates changes from one branch into the branch currently checked out.

```bash
git switch main
git merge feature/data-ingestion
```

If Git can combine the changes automatically, it completes the merge. If conflicting edits need human attention, Git pauses and asks you to resolve the conflict.

### 7. Resolving merge conflicts

A merge conflict occurs when Git cannot automatically reconcile competing changes.

A typical workflow is:

```bash
git status
```

Open each conflicted file and look for markers similar to:

```text
<<<<<<< HEAD
Current branch content
=======
Incoming branch content
>>>>>>> feature/data-ingestion
```

Edit the file to retain the intended final content and remove the conflict markers. Then:

```bash
git add <resolved-file>
git commit
```

The exact conflict-resolution workflow depends on whether the merge was started with `git merge`, `git pull`, or another operation. Check `git status` before proceeding.

### 8. Working with a remote repository

A remote repository allows local commits to be shared with GitHub.

```bash
git remote -v
git fetch origin
git pull origin main
git push origin main
```

- `git remote -v` displays configured remote URLs.
- `git fetch origin` downloads remote updates without integrating them into the current branch.
- `git pull origin main` fetches and integrates updates from the remote `main` branch.
- `git push origin main` publishes local commits to the remote `main` branch.

## 🧰 Git command reference

The following is a reference of useful commands for the workflows covered by this tutorial. It is a learning reference, not a claim that every command below appears in the repository's commit history.

| Command | What it does |
|---|---|
| `git init` | Initializes a Git repository in the current directory. |
| `git clone <url>` | Downloads a remote repository and its history. |
| `git status` | Shows branch and working-tree status. |
| `git add <file>` | Stages a selected file. |
| `git add .` | Stages changes under the current directory. |
| `git diff` | Shows unstaged changes. |
| `git diff --staged` | Shows staged changes. |
| `git commit -m "message"` | Creates a commit from staged changes. |
| `git log --oneline` | Shows compact commit history. |
| `git log --oneline --graph --all` | Displays a graph of available branch history. |
| `git branch` | Lists local branches. |
| `git switch <branch>` | Switches to an existing branch. |
| `git switch -c <branch>` | Creates and switches to a branch. |
| `git merge <branch>` | Merges the specified branch into the current branch. |
| `git fetch origin` | Fetches remote updates. |
| `git pull origin main` | Fetches and integrates the remote `main` branch. |
| `git push origin main` | Pushes local `main` commits to the remote. |
| `git remote -v` | Lists configured remotes. |
| `git stash` | Temporarily stores uncommitted tracked changes. |
| `git stash pop` | Reapplies the latest stash and removes it from the stash list if successful. |
| `git restore <file>` | Discards unstaged changes in a file. Use carefully. |
| `git rm --cached <file>` | Removes a file from Git's index but keeps the local file. |

### Inspecting project history

```bash
git log --oneline
git log --oneline --graph --decorate --all
git show <commit-id>
```

These commands help inspect commit messages, branch relationships, and the changes recorded in a particular commit.

## 🚀 Getting started

### Prerequisites

- [Git](https://git-scm.com/downloads) installed on your machine.
- A terminal such as macOS Terminal, Linux Terminal, or Windows PowerShell.
- A [GitHub account](https://github.com/).

Check your Git installation:

```bash
git --version
```

### Clone this repository

```bash
git clone https://github.com/shubhamthakur9771/Git_Tutorial.git
cd Git_Tutorial
```

### Inspect the repository

```bash
git status
git branch
git log --oneline --graph --all
git remote -v
```

### Try a small practice change

```bash
echo "Practicing Git changes" >> data_ingest.txt
git status
git diff
git add data_ingest.txt
git diff --staged
git commit -m "Practice tracking and committing changes"
```

The practice commit changes your local clone. Push only if you intend to publish your changes to the remote repository.

## 🔗 Useful resources

| Resource | Description |
|---|---|
| [Git official website](https://git-scm.com/) | Official Git website and downloads. |
| [Git documentation](https://git-scm.com/doc) | Official reference documentation. |
| [Pro Git book](https://git-scm.com/book/en/v2) | Free book covering Git concepts and workflows. |
| [Git reference](https://git-scm.com/docs) | Detailed command documentation. |
| [GitHub Docs](https://docs.github.com/en/get-started/using-git/about-git) | Learn how Git works with GitHub. |
| [GitHub Skills](https://skills.github.com/) | Interactive GitHub learning exercises. |
| [Learn Git Branching](https://learngitbranching.js.org/) | Interactive visual practice for branches and merges. |
| [GitHub repository](https://github.com/shubhamthakur9771/Git_Tutorial) | Source repository for this tutorial. |

## 👨‍💻 Author

**Shubham Kumar**

- GitHub: [@shubhamthakur9771](https://github.com/shubhamthakur9771)
- Repository: [Git_Tutorial](https://github.com/shubhamthakur9771/Git_Tutorial)

---

<div align="center">

  **Learn by doing. Track every change. Understand your history.**

  <sub>Maintained as a hands-on Git learning repository.</sub>

</div>
