# 🚀 Automated Docker Build & Push Workflow  
### Flask Application with GitHub Actions CI/CD

This project demonstrates how to:

- Build a simple Flask web application
- Containerize it using Docker
- Automate Docker image build and push using GitHub Actions
- Push the image to Docker Hub automatically on every push to the `main` branch

This is a beginner-friendly DevOps CI/CD pipeline project.

---

## 📌 Project Overview

Whenever code is pushed to the `main` branch:

1. GitHub Actions automatically starts
2. Docker image is built in the cloud
3. Docker image is pushed to Docker Hub
4. The CI/CD pipeline completes successfully

No manual Docker build is required.

---

## 🗂 Project Structure

```
Automated-Docker-Build-and-Push-WorkFlow/
│
├── .github/
│   └── workflows/
│       └── docker.yml        # GitHub Actions workflow
│
├── app.py                    # Flask application
├── requirements.txt          # Python dependencies
├── Dockerfile                # Docker configuration
└── README.md                 # Project documentation
```

---

## 🐍 Flask Application (app.py)

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Flask Docker CI/CD Working 🚀"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## 📦 Requirements (requirements.txt)

```
flask==3.0.2
```

Version locking ensures stable and repeatable builds.

---

## 🐳 Dockerfile

```dockerfile
FROM python:3.10

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

This Dockerfile:

- Uses official Python image
- Copies project files
- Installs dependencies
- Exposes port 5000
- Runs the Flask application

---

## ⚙ GitHub Actions Workflow

Location:

```
.github/workflows/docker.yml
```

Workflow file:

```yaml
name: Docker Build and Push

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and Push Image
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: Ananya838/flask-docker-app:latest
```

This workflow:

- Runs when code is pushed to `main`
- Logs into Docker Hub securely
- Builds the Docker image
- Pushes it to Docker Hub automatically

---

## 🔐 Required GitHub Secrets

Before the workflow works, add these secrets:

Go to:
Repository → Settings → Secrets and variables → Actions → New repository secret

Add:

### 1️⃣ DOCKER_USERNAME
Your Docker Hub username

### 2️⃣ DOCKER_PASSWORD
Your Docker Personal Access Token (not your actual password)

---

## 🚀 How CI/CD Works in This Project

1. Developer pushes code
2. GitHub Actions creates a virtual machine
3. Docker image is built using Dockerfile
4. Image is pushed to Docker Hub
5. Process completes automatically

This is called Continuous Integration & Continuous Deployment (CI/CD).

---

## 🧪 How to Run Locally (Optional)

If Docker is installed:

Build the image:

```
docker build -t flask-app .
```

Run the container:

```
docker run -p 5000:5000 flask-app
```

Open in browser:

```
http://localhost:5000
```

---

## 🏆 What This Project Demonstrates

- Docker containerization
- Flask web development
- GitHub Actions automation
- CI/CD pipeline implementation
- Secure secret management
- Docker Hub integration

---

## 👩‍💻 Author

Ananya838

GitHub Repository:
https://github.com/Ananya838/Automated-Docker-Build-and-Push-WorkFlow
