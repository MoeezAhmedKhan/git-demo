# Git Deep Learning Guide

---

## 📌 Step 1: Git Basic Workflow

* Make changes locally (write or edit code).
* `git add` → Put changes into staging area.
* `git commit` → Save changes in local history.
* `git push` → Send changes to GitHub.
* `git pull` → Bring other developers’ changes from GitHub to your local system.

---

## 📌 Step 2: Branches and Pull Requests (PR)

* **main** → Production (live code).
* **uat** → For testing (QA / UAT team).
* **development** → Developers’ main working branch.
* **alpha** → Temporary branch from development (for quick testing).

### Team Workflow Example:

* Frontend developer → works on `alpha-frontend`
* Backend developer → works on `alpha-backend`
* Both merge into **development** via PR.
* When development is stable → PR to **uat**.
* If UAT passes → PR to **main**.

⚡ **PR (Pull Request)** = Code review + approval before merging.

---

## 📌 Step 3: Repo Setup

### 🔹 Scenario 1: New Repo (local → GitHub)

```bash
mkdir git-practice
cd git-practice
git init
git remote add origin <repo-url>

echo "This is README" >> README.md
git add .
git commit -m "Initial commit"

git branch -M main
git push -u origin main
```

### 🔹 Scenario 2: Existing Repo (clone from GitHub)

```bash
git clone <repo-url>
cd <repo-name>

git branch -a          # see all branches
git checkout main      # switch to main
```

---

## 📌 Step 4: Create UAT and Development Branches

```bash
# Create UAT from main
git checkout main
git checkout -b uat
git push -u origin uat

# Create development from uat
git checkout uat
git checkout -b development
git push -u origin development
```

---

## 📌 Step 5: Create Alpha Branch

```bash
# Start from development
git checkout development
git pull origin development   # update first

# Create alpha branch
git checkout -b alpha
git push -u origin alpha
```

---

## 📌 Step 6: Pull Request Workflow

1. On GitHub → Create PR:
   **Source = alpha** → **Target = development**
2. After review → Merge into development.
3. When stable → **development → PR → uat**.
4. After testing → **uat → PR → main**.

---

## 📌 Step 7: Branch Protection Rules

On GitHub → Settings → Branch protection rules:
✅ Require Pull Request before merging
✅ Restrict who can push (especially `main` and `uat`)
✅ Block force pushes
✅ Block branch deletions

---

## 📌 Step 8: Tags (Release Points)

Tags mark release versions for production deployment.

```bash
git tag v1.0
git push origin v1.0
```

---

## 📌 Step 9: Common Useful Commands

```bash
git clone <repo-url>          # Download repo
git fetch                     # Fetch all updates
git branch -a                 # List all branches
git checkout <branch>         # Switch branch
git pull origin <branch>      # Get latest changes
git log --oneline --graph     # Clean commit history
```

---

## 📌 Step 10: Handling Merge Conflicts

If you see:

```bash
<<<<<<< alpha
// This is splash screen..
=======
// This is splash screen.
>>>>>>> main
```

👉 Keep only the correct line and remove conflict markers:

```bash
// This is splash screen..
```

Then resolve:

```bash
git add .
git commit -m "Resolved conflict"
git push
```

---

## 📌 Step 11: Best Practices

* Use clear commit messages (e.g., Added login validation, Fixed API bug).
* Always pull latest changes before starting new work.
* Keep PRs small and focused (easy to review).
* Never push directly to **main**.
* Regularly sync feature/alpha branches with **development**:

```bash
git checkout alpha
git pull origin development
```

---

## 🚀 Summary (Industry Standard Flow)

```
alpha → PR → development → PR → uat → PR → main
```

✅ Direct push to `main` is blocked.
✅ Only tested and approved code reaches production.
