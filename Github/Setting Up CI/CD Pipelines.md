# **🚀 Setting Up CI/CD Pipelines  Project**

A **CI/CD (Continuous Integration/Continuous Deployment) pipeline** automates the process of testing, building, and deploying your application. We'll set up a **GitHub Actions-based CI/CD pipeline** that ensures project is always production-ready.

---

# **✅ Step 1: Understanding CI/CD Workflow**

### **🔹 Continuous Integration (CI)**

1️⃣ Developers push code to GitHub.

2️⃣ Automated tests run on each push.

3️⃣ If tests pass, the code is  **merged** .

### **🔹 Continuous Deployment (CD)**

4️⃣ After merging, the app **builds** and **deploys** automatically.

5️⃣ Users get the latest version  **without manual intervention** .

---

# **✅ Step 2: Create a GitHub Actions Workflow**

GitHub Actions is a **free automation tool** to set up a  **CI/CD pipeline** .

## **📌 2.1 Create `.github/workflows/ci-cd.yml`**

In your GitHub repository, create a new file:

📁 `.github/workflows/ci-cd.yml`

---

# **🚀 Example CI/CD Pipeline (Node.js & React App)**

This pipeline:
✅ Runs tests on  **every push & pull request** .

✅ Deploys to **GitHub Pages or a server** when code is merged into `main`.

```yaml
name: CI/CD Pipeline

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

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Build project
        run: npm run build

      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main'
        run: |
          npm install -g gh-pages
          npm run deploy
```

✅ **Breakdown of this pipeline:**

1️⃣ **Checks out the latest code** (`actions/checkout`).

2️⃣ **Installs dependencies** (`npm install`).

3️⃣ **Runs tests** (`npm test`).

4️⃣ **Builds the project** (`npm run build`).

5️⃣ **Deploys** if the branch is `main`.

---

# **✅ Step 3: Deploying to Different Platforms**

## **📌 3.1 Deploying to GitHub Pages**

For  **React apps** , modify `package.json`:

```json
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

✅ The GitHub Actions pipeline will **automatically deploy** when you push to `main`.

---

## **📌 3.2 Deploying a Node.js App to a Server (SSH)**

If you're deploying a  **Node.js backend** , update `.github/workflows/ci-cd.yml`:

```yaml
  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Deploy to Server
        uses: appleboy/ssh-action@v0.1.7
        with:
          host: ${{ secrets.SERVER_IP }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          script: |
            cd /var/www/myapp
            git pull origin main
            npm install
            pm2 restart myapp
```

✅ This will:

1. SSH into the **remote server**
2. **Pull the latest code**
3. **Restart the app using PM2**

---

## **📌 3.3 Deploying to Docker & AWS**

To deploy using  **Docker** , modify `.github/workflows/ci-cd.yml`:

```yaml
  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Log in to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build Docker image
        run: docker build -t myapp .

      - name: Push Docker image
        run: docker push myapp
```

✅ Then, AWS **EC2** or **ECS** can pull and run the new image.

---

# **🚀 Summary: Automated CI/CD Pipeline**

* ✅ **Code is pushed to GitHub**
* ✅ **Tests run automatically**
* ✅ **Builds the app**
* ✅ **Deploys to GitHub Pages, a server, or Docker**
