---
title: "Git & GitHub"
datePublished: Fri Sep 26 2025 07:14:34 GMT+0000 (Coordinated Universal Time)
cuid: cmg0ib0qs000c02l8afvvfti9
slug: git-and-github
tags: codewithnini

---

## 📘 Git & GitHub for Automation Testers

## 🔹 1. What is Git?

* **Git** is a **distributed version control system**.
    
* It helps track changes in code, collaborate with teams, and maintain different versions of a project.
    
* You work locally in your machine (Git repo), then push changes to a **remote repo** (e.g., GitHub, GitLab, Bitbucket).
    

👉 **Why testers need Git?**

* To store **automation test scripts** (Selenium, RestAssured, Cypress, Playwright, etc.).
    
* To work in a **team** (developers + testers).
    
* To integrate with **CI/CD tools (Jenkins, GitHub Actions)**.
    
* To maintain **version history** of test cases & frameworks.
    

---

## 🔹 2. What is GitHub?

* **GitHub** = cloud-based Git repository hosting service.
    
* Provides UI + collaboration features like Pull Requests, Code Reviews, Issues, Actions (CI/CD).
    

👉 **Why testers need GitHub?**

* Store and share automation frameworks with team.
    
* Run **GitHub Actions pipelines** (for test execution).
    
* Collaborate with Dev/QA team using Pull Requests.
    
* Manage bugs/issues linked with test failures.
    

---

## 🔹 3. Git Workflow for Testers

A common workflow you’ll use daily:

1. **Clone project** from GitHub
    
    ```bash
    git clone <repo-url>
    ```
    
    Example: cloning automation framework repo.
    
2. **Create new branch** (never work on main directly)
    
    ```bash
    git checkout -b feature/add-login-tests
    ```
    
3. **Make changes** → Add new test scripts, update framework.
    
4. **Check status**
    
    ```bash
    git status
    ```
    
5. **Stage changes**
    
    ```bash
    git add .
    ```
    
6. **Commit changes**
    
    ```bash
    git commit -m "Added login test cases"
    ```
    
7. **Push branch to GitHub**
    
    ```bash
    git push origin feature/add-login-tests
    ```
    
8. **Create Pull Request (PR)** in GitHub → reviewed by team → merged into `main`.
    

---

## 🔹 4. Common Git Commands for Testers

| Command | Purpose | Example |
| --- | --- | --- |
| `git clone <url>` | Copy repo from GitHub to local | `git clone` [`https://github.com/user/project.git`](https://github.com/user/project.git) |
| `git status` | Show changed files | `git status` |
| `git add <file>` | Stage file for commit | `git add` [`LoginTest.java`](http://LoginTest.java) |
| `git add .` | Stage all files | `git add .` |
| `git commit -m "msg"` | Save changes | `git commit -m "Added test cases"` |
| `git checkout -b <branch>` | Create new branch | `git checkout -b bugfix/login-issue` |
| `git checkout <branch>` | Switch branch | `git checkout main` |
| `git pull origin main` | Get latest changes | `git pull origin main` |
| `git push origin <branch>` | Push branch to remote | `git push origin feature/cart-tests` |
| `git log --oneline` | Show commit history | `git log --oneline` |
| `git diff` | Show code differences | `git diff` |

---

## 🔹 5. Branching Strategy (Important in Companies)

Automation testers follow **branching models**:

* **main/master** → Stable code (only reviewed code is merged).
    
* **develop** → For ongoing development/testing.
    
* **feature branches** → New test scripts or framework changes.
    
* **bugfix branches** → Fixing test failures/defects.
    

👉 Example for automation project:

* `feature/login-tests` → you add login scripts.
    
* `feature/api-order-tests` → API automation test cases.
    

---

## 🔹 6. GitHub Features for Testers

1. **Pull Requests (PRs)** → code review before merge.
    
2. **Issues** → bug tracking & linking with test failures.
    
3. **Projects** → Agile boards (Kanban/Scrum for QA tasks).
    
4. **GitHub Actions** → run Selenium/TestNG/RestAssured tests automatically.
    

---

## 🔹 7. Real Use Cases in Automation Testing

✅ **Selenium Framework**:

* Store Selenium + TestNG/Maven framework in GitHub.
    
* Team pulls latest test code daily.
    
* Jenkins/GitHub Actions runs tests automatically on push.
    

✅ **API Testing with RestAssured**:

* Store API test cases in Git repo.
    
* Run them in CI/CD whenever backend deploys new code.
    

✅ **Test Data Management**:

* Keep property files, JSON data, Excel test data in repo.
    
* Everyone uses same version-controlled data.
    

✅ **Version Control**:

* Rollback to earlier commit if new test cases are failing.
    

---

## 🔹 8. Interview-Focused Explanation

**Q: Why should an automation tester use Git/GitHub?**  
👉 "As a tester, I use Git/GitHub to collaborate with the team, maintain version-controlled automation frameworks, and integrate test execution with CI/CD pipelines. It ensures everyone works on the latest code, avoids conflicts, and keeps a clean history of test script changes."

---

✅ **Summary for Testers**:

* **Git** = Version control tool (local).
    
* **GitHub** = Remote repo + collaboration + CI/CD.
    
* You’ll use Git commands daily to manage automation frameworks.
    
* In interviews, focus on **branching, merging, PRs, CI/CD integration**.
    

# 📘 Git & GitHub Cheat Sheet for Automation Testers

---

## 🔹 1. Setup & Configuration

| Command | Meaning | Example (Automation Use Case) |
| --- | --- | --- |
| `git config --global` [`user.name`](http://user.name) `"YourName"` | Set global username | Identify yourself for commits |
| `git config --global` [`user.email`](http://user.email) `"`[`you@email.com`](mailto:you@email.com)`"` | Set global email | Required for commit author |
| `git init` | Initialize new repo | Start a new Selenium framework repo |
| `git clone <repo-url>` | Clone remote repo | Download existing automation project from GitHub |

---

## 🔹 2. Checking Status & History

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git status` | Show changed files | See which test scripts are modified |
| `git log --oneline` | View commit history | Check past changes in test framework |
| `git diff` | Show code differences | See what changed in [`LoginTest.java`](http://LoginTest.java) |

---

## 🔹 3. Staging & Committing

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git add <file>` | Stage a single file | `git add` [`LoginTest.java`](http://LoginTest.java) |
| `git add .` | Stage all files | Add all updated Selenium test scripts |
| `git commit -m "message"` | Commit staged changes | `"Added login test cases with TestNG"` |

---

## 🔹 4. Branching & Switching

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git branch` | List branches | Check current branches (`main`, `develop`, `feature/login`) |
| `git checkout -b <branch>` | Create new branch | `git checkout -b feature/api-tests` |
| `git checkout <branch>` | Switch branch | Move from `develop` → `main` |
| `git branch -d <branch>` | Delete branch | Remove unused `bugfix/test-data` branch |

---

## 🔹 5. Pushing & Pulling (Sync with GitHub)

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git pull origin main` | Get latest code from GitHub | Pull updated API tests written by teammate |
| `git push origin <branch>` | Push branch to remote | Push your `feature/cart-tests` to GitHub |
| `git fetch` | Download branch info (no merge) | See if `develop` branch has new changes |

---

## 🔹 6. Merging & Collaboration

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git merge <branch>` | Merge branch into current | Merge `feature/login-tests` into `develop` |
| `git rebase <branch>` | Reapply commits on top | Keep clean history for test framework |
| `git pull --rebase` | Pull with rebase | Avoid conflicts in automation repo |
| **GitHub UI → Pull Request (PR)** | Request merge with review | Submit Selenium test scripts for review |

---

## 🔹 7. Undo & Reset

| Command | Meaning | Example Use Case |
| --- | --- | --- |
| `git reset --hard <commit>` | Reset repo to old commit | Rollback broken test scripts |
| `git revert <commit>` | Undo commit safely | Revert a failed API test addition |
| `git checkout -- <file>` | Discard local changes | Remove unwanted edits in [`config.properties`](http://config.properties) |

---

## 🔹 8. GitHub-Specific (Cloud Repo)

| Feature | Purpose | Example Use Case |
| --- | --- | --- |
| **Issues** | Bug tracking | Log bug for failed automation test |
| **Pull Requests (PRs)** | Code review & merge | Submit `feature/order-tests` for team review |
| **Actions (CI/CD)** | Run pipelines | Run Selenium tests on each PR merge |
| **Wiki** | Documentation | Maintain automation framework setup steps |

---

# ✅ Quick Real-World Automation Workflow

1. Clone repo:
    
    ```bash
    git clone https://github.com/company/automation-framework.git
    ```
    
2. Create branch:
    
    ```bash
    git checkout -b feature/add-login-tests
    ```
    
3. Add new Selenium test → stage & commit:
    
    ```bash
    git add LoginTest.java
    git commit -m "Added login test cases"
    ```
    
4. Push branch:
    
    ```bash
    git push origin feature/add-login-tests
    ```
    
5. Create **Pull Request in GitHub** → reviewed → merged.
    
6. Jenkins/GitHub Actions picks updated code → runs tests.
    

---

⚡ This cheat sheet gives **everything an automation tester needs daily**: setup → commit → branch → sync → PR → CI/CD.