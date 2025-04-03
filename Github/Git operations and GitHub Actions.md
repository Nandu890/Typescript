# **🚀 Git Operations & GitHub Actions: A Complete Guide**

Git is essential for version control, while GitHub Actions automates workflows like testing, deployment, and CI/CD. This guide covers **Git operations** and how to **integrate GitHub Actions** into your project.

---

# **✅ 1. Git Basics (Essential Commands)**

### **🔹 1.1 Initializing a Git Repository**

```sh
git init
```

✅ This creates a new Git repository in your project folder.

---

### **🔹 1.2 Cloning a Repository**

```sh
git clone <repo-url>
```

✅ Copies a remote repository to your local machine.

Example:

```sh
git clone https://github.com/user/repository.git
```

---

### **🔹 1.3 Staging and Committing Changes**

```sh
git add <filename>   # Stage a specific file
git add .            # Stage all changes
git commit -m "Added new feature"
```

✅ Stages and saves changes with a commit message.

---

### **🔹 1.4 Checking Status & Logs**

```sh
git status    # Shows modified/untracked files
git log       # Shows commit history
```

✅ Useful for tracking changes and debugging issues.

---

### **🔹 1.5 Pushing Changes to Remote**

```sh
git push origin main  # Push to the main branch
```

✅ Sends committed changes to GitHub.

---

### **🔹 1.6 Pulling Updates**

```sh
git pull origin main
```

✅ Fetches the latest changes from the remote repository.

---

### **🔹 1.7 Creating & Switching Branches**

```sh
git branch feature-branch   # Create a new branch
git checkout feature-branch # Switch to the new branch
git switch feature-branch   # Alternative way to switch
```

✅ Use branches for new features or bug fixes.

---

### **🔹 1.8 Merging Branches**

```sh
git checkout main       # Switch to main branch
git merge feature-branch # Merge changes from feature branch
```

✅ Integrates changes from another branch.

---

### **🔹 1.9 Resolving Merge Conflicts**

If you see a  **merge conflict** , manually edit the conflicting files and mark the conflict resolution.

```sh
git add resolved-file
git commit -m "Resolved merge conflict"
```

---

### **🔹 1.10 Undoing Changes**

```sh
git reset --soft HEAD~1  # Undo last commit (keep changes)
git reset --hard HEAD~1  # Undo last commit (delete changes)
```

✅ Reverts changes safely or forcefully.

---

# **✅ 2. Setting Up GitHub Actions for CI/CD**

**GitHub Actions** automates workflows such as running tests, building apps, and deploying projects.

## **🔹 2.1 Creating a GitHub Actions Workflow**

1️⃣ In your GitHub repository, go to  **Actions** .

2️⃣ Click **"New workflow"** → **"Set up a workflow yourself"**

3️⃣ Create a `.github/workflows/ci.yml` file in your project.

---

## **🔹 2.2 Example: Basic CI Workflow**

A simple workflow that runs on every push:

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install dependencies
        run: npm install

      - name: Run Tests
        run: npm test
```

✅ This workflow:

1. Runs on **push or pull request** to `main`.
2. **Checks out the code** from GitHub.
3. **Installs dependencies** (`npm install`).
4. **Runs tests** (`npm test`).

---

## **🔹 2.3 Example: Deploying a React App to GitHub Pages**

Deploy a React app using GitHub Actions:

1️⃣ Install `gh-pages` in your project:

```sh
npm install gh-pages --save-dev
```

2️⃣ Add the following to `package.json`:

```json
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

3️⃣ Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy React App

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install dependencies
        run: npm install

      - name: Build project
        run: npm run build

      - name: Deploy to GitHub Pages
        run: npm run deploy
```

✅ Automatically deploys the app when changes are pushed to `main`.

---

## **🔹 2.4 Example: Auto-Release Using GitHub Actions**

Automatically create a release when you push new changes.

Create `.github/workflows/release.yml`:

```yaml
name: Auto Release

on:
  push:
    tags:
      - "v*"

jobs:
  release:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Create a GitHub Release
        uses: actions/create-release@v1
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          body: "New release available!"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

✅ Creates a **GitHub Release** whenever you push a new tag (`v1.0.0`).

---

## **🔹 2.5 Example: Deploying a Node.js App to Heroku**

1️⃣ Add **Heroku API Key** to GitHub Secrets (`HEROKU_API_KEY`).

2️⃣ Create `.github/workflows/heroku.yml`:

```yaml
name: Deploy to Heroku

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install dependencies
        run: npm install

      - name: Login to Heroku
        run: echo ${{ secrets.HEROKU_API_KEY }} | docker login --username=_ --password-stdin registry.heroku.com

      - name: Push to Heroku
        run: git push heroku main
```

✅ Deploys the app to **Heroku** on every push to `main`.

---
