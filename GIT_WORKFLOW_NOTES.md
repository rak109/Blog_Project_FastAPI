# Git and Terminal Study Notes

These notes explain the Git commands used while setting up this FastAPI project and adding tutorial work to your GitHub repository.

## 1. Open the project folder in PowerShell

Move into the folder that contains the `.git` directory:

```powershell
cd C:\Users\HPADMIN\Documents\BLOG_Project_FastAPI\Blog_Project_FastAPI
```

Open that folder in VS Code with a space between `code` and the dot:

```powershell
code .
```

`code.` is not a valid command. The dot means "open the current folder."

If Git says `fatal: not a git repository`, the terminal is probably in the wrong folder. Use `pwd` to see the current location, then `cd` into the repository folder.

## 2. Set your commit name and email

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global --list
```

These values label your commits. They do not sign you in to GitHub. GitHub authentication happens separately, often in a browser window when you push.

## 3. Clone your GitHub repository

```powershell
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
```

`git clone` downloads the repository and creates a local folder. Run later Git commands from inside that folder.

## 4. Check your repository

```powershell
git status
git branch -vv
git remote -v
git log -5 --oneline --decorate
```

- `git status` shows your current branch and changes that are not committed.
- `git branch -vv` lists local branches and shows which remote branch each one tracks.
- `git remote -v` shows the GitHub repositories connected to this local folder.
- `git log` shows recent commits.

In this project, `origin` is your GitHub repository. `tutorial` is the tutorial source repository. Use `origin` when pushing your work. Do not push to someone else's tutorial repository.

## 5. Create and switch to a branch

Start a branch for each chunk of work so it can be reviewed separately:

```powershell
git switch -c day-01-tutorial-setup
```

For the next tutorial, create a new branch from your current branch:

```powershell
git switch -c day-02-templates
```

Check which branch is active with:

```powershell
git branch
```

The `*` marks the active branch. A branch is a separate line of work; making a branch does not publish it to GitHub.

## 6. Add a tutorial repository as a remote

```powershell
git remote add tutorial https://github.com/OWNER/TUTORIAL-REPOSITORY.git
git remote -v
git fetch tutorial
```

A remote is a named connection to another Git repository. `git fetch tutorial` downloads its branch and commit information. Fetching alone does **not** copy files into your project or merge changes into your branch.

See the files stored on the tutorial's main branch:

```powershell
git ls-tree -r --name-only tutorial/main
```

Show a file from that branch without checking it out:

```powershell
git show tutorial/main:main.py
```

If Git opens a pager (a screen for viewing long output), press `q` to exit. If you see `(END)`, you are viewing output, not stuck in PowerShell.

## 7. Copy files from another branch carefully

This command was used to copy tracked files from the tutorial branch into the current branch:

```powershell
git checkout tutorial/main -- .
```

The `.` means all paths. This command also stages the copied files. If a file has the same name in both branches, the tutorial version can replace your local version. Check `git status` and review the changes before committing. Do not run it when you have uncommitted work you need to preserve.

Copying files this way copies file contents, not the tutorial's commit history. Check the source repository's license or get permission before publishing someone else's code in your repository.

## 8. Stage, review, commit, and push

First review changes:

```powershell
git status
git diff
```

Stage only the files you intend to include. For example:

```powershell
git add main.py pyproject.toml uv.lock templates static
```

Review staged changes, then commit:

```powershell
git diff --cached
git diff --cached --check
git commit -m "Add day 02 templates"
```

A commit saves a named checkpoint in your local Git history. It does not send the commit to GitHub yet.

Push a branch to your GitHub repository and set its upstream the first time:

```powershell
git push -u origin day-02-templates
```

For later pushes from that branch, this is usually enough:

```powershell
git push
```

If GitHub asks you to authenticate, complete the sign-in in the browser. Do not put your password or token into the Git remote URL.

## 9. Merge your branch into `main`

Pushing a branch does not merge it into `main`. After pushing, GitHub may show a link to create a pull request. Open the pull request, review the changes, and merge it when ready. A pull request lets you compare the branch with `main` before merging.

## 10. Stop a running command or server

- Press `Ctrl+C` in the terminal running a server to stop it.
- If a command is still running, `Ctrl+C` normally interrupts it.
- If Git is showing paged output, press `q` instead.
- When PowerShell shows a prompt such as `PS C:\...>`, it is ready for another command.

## Current project status

At the time these notes were written:

- The active branch is `day-02-templates`.
- The day-01 branch and commit are already pushed to `origin`.
- The day-02 template changes are currently uncommitted: `main.py`, `pyproject.toml`, `uv.lock`, `static/`, and `templates/`.
- Before committing day-02, review the changes with `git status` and `git diff`.
- After committing, push with `git push -u origin day-02-templates`.
