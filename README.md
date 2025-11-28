MEAN CRUD DevOps Project
This repository contains a full‑stack CRUD application built with the MEAN stack and deployed using a complete Docker‑based DevOps pipeline on AWS EC2.

Tech stack
Frontend: Angular app built in Node and served by Nginx in Docker.

Backend: Node.js + Express + MongoDB (Mongoose) in Docker.

Database: MongoDB official Docker image.

Orchestration: Docker Compose multi‑service stack.

CI/CD: GitHub Actions building and pushing Docker images, then deploying to EC2.

Cloud: AWS EC2 Ubuntu instance running Docker and Docker Compose.

Local setup and run
Clone repository
git clone https://github.com/Akhiranandh/crud-dd-task-mean-app.git
cd crud-dd-task-mean-app

Start full stack with Docker Compose
docker-compose up -d --build

Access services locally


Angular UI (via Nginx): http://localhost

API base URL: http://localhost/api

Tutorials API example:

GET http://localhost/api/tutorials

POST http://localhost/api/tutorials

To stop everything:
docker-compose down

Project structure
frontend/ – Angular application with Dockerfile for multi‑stage build (Node build + Nginx serve).

backend/ – Node.js + Express + MongoDB API with Dockerfile.

backend/app/routes/tutorial.routes.js – Express router for /api/tutorials CRUD endpoints.

backend/server.js – Express server mounting the router under /api.

docker-compose.yml – Defines frontend, backend, and mongo services and networking.

.github/workflows/deploy.yml – GitHub Actions CI/CD pipeline configuration.
AWS EC2 deployment
Launch EC2 instance

OS: Ubuntu (e.g., 22.04).

Type: t3.micro.

Open ports in Security Group: 22, 80, 3000, 27017.

Install Docker and Docker Compose
sudo apt update
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker ubuntu
Clone repo and start stack
git clone https://github.com/Akhiranandh/crud-dd-task-mean-app.git
cd crud-dd-task-mean-app
sudo docker-compose up -d --build
Access deployed app

Public URL: http://<EC2_PUBLIC_IP> (Angular UI via Nginx).

API (from EC2): http://localhost:3000/api/tutorials.

For this deployment the public IP is:

http://18.60.239.233

CI/CD pipeline (GitHub Actions)
Workflow file: .github/workflows/deploy.yml

Pipeline behaviour:

Trigger: every push to the main branch.

Steps:

Checkout repository code.

Login to Docker Hub using GitHub Secrets (DOCKER_USERNAME, DOCKER_PASSWORD).

Build and push backend image from ./backend to Docker Hub.

Build and push frontend image from ./frontend to Docker Hub.

SSH into the EC2 instance using secrets (VM_HOST, VM_USERNAME, VM_SSH_KEY).

On EC2:

cd crud-dd-task-mean-app

git pull

docker compose pull

docker compose up -d --build

This provides an automated pipeline: pushing code to main automatically builds images, updates them on EC2, and restarts the containers.


### CI/CD workflow

![GitHub Actions workflow](screenshots/actions.png)

### Docker Hub images

![Docker Hub images](screenshots/docker-hub.png)

### Deployed application UI

![Live MEAN app UI](screenshots/app-ui.png)

### Nginx / Docker Compose setup

![Nginx and Docker Compose](screenshots/nginx-compose.png)
