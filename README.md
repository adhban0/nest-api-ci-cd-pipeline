# 🚀 NestJS CI/CD Pipeline with GitHub Actions & Docker

A production-ready NestJS backend with automated CI/CD using **GitHub Actions**, **Docker**, and **Docker Compose**.  
This setup ensures automated builds, testing, Docker image publishing, and **zero-downtime deployment** to production.

---

## 📂 Project Structure

```
.
├── src/                 # NestJS application source code
├── Dockerfile           # Docker image definition
├── docker-compose.yml   # Docker Compose for local/prod setup
├── .github/workflows/   # GitHub Actions workflows
└── README.md            # Documentation
```

---

## ⚡ Features

- ✅ Automated build & test on Pull Requests
- ✅ Docker image creation & push to Docker Hub
- ✅ Production deployment via GitHub Actions + SSH
- ✅ Multi-stage Docker builds (optimized image size)
- ✅ Environment-specific configs (staging/prod)

---

## 🛠️ Setup Guide

### 1️⃣ Clone the Repository
```bash
  git clone https://github.com/ThimiraSadeesha/nest-api-ci-cd-pipeline.git
  cd nest-api-ci-cd-pipeline
```

---

### 2️⃣ Install Dependencies (Optional: Local Development)
```bash
  npm install
  npm run start:dev
```

---

### 3️⃣ Create a Docker Hub Account
Before setting up GitHub Environments, make sure you have a **Docker Hub account**:
- Sign up at [https://hub.docker.com](https://hub.docker.com)
- Create a **new public repository** (e.g., `nest-api-ci-cd-pipeline`)
- You will need your **Docker Hub username** and **password/token** in the next step


---

### 4️⃣ Environment Configuration
Create a `Repository Environment` in the GitHub repo:

1. Go to **Settings → Environments → New environment**
2. Name the environment `production`


---

### 5️⃣ GitHub Secrets & Environments

In your **GitHub repo settings**, under `production` environment, add the following secrets:

- `DOCKER_USERNAME` → Your Docker Hub username
- `DOCKER_PASSWORD` → Your Docker Hub password or token
- `SERVER_IP` → Your production server IP
- `SERVER_USER` → Your server SSH username
- `SERVER_SSH_KEY` → Private SSH key for deployment


---

### 6️⃣ Docker Setup (Local)
```bash
  docker-compose up --build -d
```
This will build and run the app in a container at `http://localhost:3000`.

---

### 7️⃣ CI/CD Workflow

- **Pull Request (PR)** → Runs build & test workflow (no deploy)
- **Main branch push** → Builds Docker image, pushes to Docker Hub, deploys to production server

📸 *Screenshot Example – GitHub Actions Workflow:*  
![GitHub Actions](docs/images/github-actions.png)

---

### 8️⃣ Deploy to Production Manually (Optional)
If you want to deploy manually:
```bash
  ssh user@your-server-ip
  docker pull your-docker-hub-username/nest-api-ci-cd-pipeline:latest
  docker stop nest-api-prod || true
  docker rm nest-api-prod || true
  docker run -d   --restart unless-stopped   --name nest-api-prod   -p 3000:3000   -e NODE_ENV=production   your-docker-hub-username/nest-api-ci-cd-pipeline:latest
```

---

## 📦 Docker Image

Available on Docker Hub:  
👉 `your-docker-hub-username/nest-api-ci-cd-pipeline:latest`

---

## 📌 Tech Stack
- [NestJS](https://nestjs.com/) – Backend framework
- [Docker](https://www.docker.com/) – Containerization
- [GitHub Actions](https://github.com/features/actions) – CI/CD automation
- [Docker Hub](https://hub.docker.com/) – Image registry

---

## 🚀 Result
By simply **merging code into `main`**, the backend is automatically:
- Tested ✅
- Built into a Docker image ✅
- Pushed to Docker Hub ✅
- Deployed to production ✅  


# Test 1
