---
layout: default
title: "Week 1: Git Introduction"
---

# Git Introduction


This project will guide you through some of the more common features of Git used for project development — specifically remotes, pushing/pulling, and branches.

---

## Part 0: Forking & Cloning the Repo

1. Visit [https://github.com/som1shi/sp26-plextech-fswd-intro-projects](https://github.com/som1shi/sp26-plextech-fswd-intro-projects)
2. Click the **Fork** button in the upper right corner
3. Make sure the Owner is your GitHub account, then click **Create fork**
4. On your forked repo's main page, click the green **`<> Code`** button
5. Copy the HTTPS link, then run in a new local folder:

```bash
git clone <your-forked-repo-url>
```

You should now see the starter code available locally.

---

## Part 1 — Pushing & Pulling

> Work in **pairs** for this section. Assign one person as **Person A** and one as **Person B**. Work side-by-side to see the full Git collaboration flow.

### Person B Only

Clone down Person A's repository (make sure Person A has invited you first):

1. Navigate to Person A's forked repo and click **`<> Code`**
2. Copy the HTTPS link
3. In a new folder outside your own repo, run:

```bash
git clone <person-a-repo-url>
```

Now, inside Person A's `Git Intro/` folder, run `git log` and save a screenshot there.

Stage, commit, and push your screenshot:

```bash
git status
git add "Git Intro/<screenshot-filename>"
git commit -m "image added"
git push origin main
```

---

### Person A Only

Do the same workflow as Person B:

1. In your `Git Intro/` folder, run `git log` and save a screenshot
2. Then stage, commit, and try to push:

```bash
git fetch --all
git status
git add "Git Intro/<screenshot-filename>"
git commit -m "image added"
git push origin main
```

You should get an error like: **"Updates were rejected because the remote contains work that you do not have locally."**

This means Person B's push came in first. Fix it by pulling first:

```bash
git pull origin main
git push origin main
```

No errors this time!

---

## Part 2 — Branching

When working on larger projects, you'll work on a separate **branch** per feature. This keeps independent lines of development clean.

### Person B Only

Suppose Person A wrote `foo.py` — a function that prints `"Foo"` if input is a multiple of 3 and `"Bar"` otherwise — but it only works for positive numbers up to 30. Your job is to fix it.

```bash
git pull origin main
git checkout -b bug-fix
```

Fix the function in `foo.py`, then:

```bash
git add foo.py
git commit -m "fix foo.py to handle all integers"
git push origin bug-fix
```

---

### Person A Only

Person B fixed the bug in `bug-fix`, but `main` is still broken. Open a **Pull Request** to merge it in:

1. On your GitHub repo, click **Pull requests → New pull request**
2. Set **base:** `main`, **compare:** `bug-fix`
3. Click **Create pull request**
4. Leave a review comment (e.g., "LGTM!")
5. Click **Merge pull request** and confirm

The fix is now on `main`.

> For more on branching: [Atlassian Git Branching Tutorial](https://www.atlassian.com/git/tutorials/using-branches)

---

## Submission

Push all required files to your forked repository and confirm all parts are visible on GitHub.
