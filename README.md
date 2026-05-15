### AWS DEVOPS Lab # 1  

# 🚀 End-to-End AWS DevOps Microservices Lab  

> ## (EC2 + Docker + CI/CD + Monitoring)

---

![AWS DevOps Microservices Lab Architecture](./lab_doc/791b41c0-8c67-4043-b452-4c210ebd4b70.png)

## 🧪 COMPLETE AWS DEVOPS LAB (BEGINNER → ADVANCED)

We’ll build a complete DevOps system on AWS EC2 using:

- Amazon Web Services  

- Docker 

- GitHub  

- GitHub Actions  

- Prometheus 

- Grafana  

---

## 🎯 LAB GOAL

Build a production-style DevOps environment on Amazon Web Services where you:

- Deploy a microservices-based application  

- Use Docker for containerization

- Manage code with GitHub  

- Automate delivery using GitHub Actions  

- Monitor system using Prometheus + Grafana  

- Apply Linux + Networking + Security + Debugging skills  

👉 **Final Outcome:**  

You behave like a real DevOps Engineer handling production deployment  

---

## 🧩 REAL-LIFE PRACTICAL TASKS

These are not “practice commands” — these are actual job tasks.

---

## 🧱 Infrastructure Tasks (AWS EC2)

- Launch EC2 server for application hosting  

- Configure Security Groups (open ports 22, 80, 443, 3000, 9090)  

- Connect securely using SSH keys  

- Harden server (disable password login, restrict access)  

---

## 🐧 Linux Administration Tasks

- Create users for developers (dev, qa)  

- Assign permissions to shared directories 

- Monitor CPU/memory when app is slow  

- Analyze logs when service crashes (`/var/log`, `journalctl`)  

- Write backup script: 

```
backup-$(date).tar.gz
```

- Kill high CPU processes  

- Manage services using systemd  

---

## 🔧 Git & Collaboration Tasks

- Initialize project repo on EC2 

- Push code to GitHub  

- Create feature branches (feature/login) 

- Resolve merge conflicts  

- Use git revert for production rollback  

- Tag releases (v1.0, v2.0)  

---

## 🐳 Docker Tasks

- Convert app into Docker image  

- Run container with port mapping  

- Debug container crash (`docker logs`)  

- Use volumes for persistent data  

- Build multi-container app using docker-compose  

- Push images to Docker Hub  

---

## 🧩 Microservices Tasks

- Build:

    - Frontend service  

    - Backend API 

    - Database service  

- Connect services using Docker network  

- Simulate service failure and recovery  

---

## 🔁 CI/CD Tasks

- Automate pipeline:

    - Code push → Build → Test → Deploy  

- Store secrets securely
 
- Fix failed pipelines
  
- Deploy app automatically to EC2  

---

## 🔐 Security Tasks

- Use IAM roles instead of credentials  

- Store secrets in GitHub Secrets  

- Scan images using Trivy 

- Remove hardcoded passwords  

---

## 📊 Monitoring Tasks

- Install Prometheus & Grafana:

- Monitor:

    - CPU usage  

    - Memory usage  

    - Container health  

- Detect system overload

---

## 🚨 Real Incident Simulation

- App not accessible → debug ports 

- High CPU → find process  

- Container crash → restart + logs  

- Wrong deployment → rollback  

---

## 🔄 DATA FLOW DIAGRAM (TEXT)

```
Developer → GitHub → CI/CD Pipeline → Docker Build → Docker Registry → EC2 → Running Containers → User Access

Monitoring Flow:
EC2 + Containers → Prometheus → Grafana Dashboard
```

---

## 🔍 STEP-BY-STEP FLOW

1. Developer writes code  

2. Code pushed to GitHub  

3. GitHub Actions triggers pipeline  

4. Docker image is built  

5. Image pushed to Docker Hub  

6. EC2 pulls latest image  

7. Container starts  

8. User accesses app 

9. Prometheus collects metrics  

10. Grafana visualizes system health  

---

## 🖼️ DIGITAL VISUAL ARCHITECTURE

Here is a clean architecture diagram (text-style visual)

```
                   👨‍💻 Developer
                        │
                        ▼
               ┌──────────────────┐
               │   GitHub Repo    │
               └──────────────────┘
                        │
                        ▼
         ┌────────────────────────────┐
         │   GitHub Actions (CI/CD)   │
         │ Build → Test → Dockerize   │
         └────────────────────────────┘
                        │
                        ▼
               ┌──────────────────┐
               │  Docker Registry │
               │   (Docker Hub)   │
               └──────────────────┘
                        │
                        ▼
        ┌────────────────────────────────┐
        │        AWS EC2 Server          │
        │                                │
        │  ┌───────────────┐             │
        │  │  Frontend     │ (3000)      │
        │  └───────────────┘             │
        │          │                     │
        │          ▼                     │
        │  ┌───────────────┐             │
        │  │  Backend API  │ (4000)      │
        │  └───────────────┘             │
        │          │                     │
        │          ▼                     │
        │  ┌───────────────┐             │
        │  │   Database    │ (MongoDB)   │
        │  └───────────────┘             │
        │                                │
        └────────────────────────────────┘
                        │
                        ▼
                🌐 End Users (Browser)

---------------------------------------------------

📊 MONITORING LAYER

EC2 + Containers
        │
        ▼
 ┌──────────────┐
 │ Prometheus   │ (9090)
 └──────────────┘
        │
        ▼
 ┌──────────────┐
 │ Grafana      │ (3001)
 └──────────────┘
```

## 🧠 HOW THIS LAB WORKS (IMPORTANT)

This lab simulates a real company workflow:

---

## 🔁 Continuous Loop

- Developer writes code

- CI/CD builds and deploys  

- App runs on EC2  

- Monitoring tracks system health  

- Issues occur in production  

- DevOps engineer investigates and fixes 

- Cycle repeats continuously  

---

## 🎯 FINAL UNDERSTANDING

This lab teaches you:

- Infrastructure thinking (not just commands)  

- System flow (how everything connects end-to-end) 

- Debugging real production problems  

- Automation mindset (CI/CD thinking) 

- Production-level responsibility and ownership  

---

# 🧱 PHASE 1: AWS EC2 SETUP (FOUNDATION)

## ✅ Step 1: Launch EC2 Instance
OS: Ubuntu 22.04 or Amazon Linux 2023  
Instance type: t2.micro (free tier)

### Why this matters:

- EC2 = your real Linux server in cloud

- Ubuntu = most widely used DevOps OS

- t2.micro = free lab environment

---

## ✅ Step 2: Security Group (VERY IMPORTANT)

Allow ports:

| Port      | Purpose                |
| --------- | ---------------------- |
| 22        | SSH access             |
| 80        | HTTP web traffic       |
| 443       | HTTPS secure traffic   |
| 3000–5000 | Apps (Docker services) |
| 9090      | Prometheus             |
| 3001      | Grafana                |

### Why this is critical:

Security Group = firewall of AWS

👉 It controls WHO can access your server
---

## ✅ Step 3: Connect via SSH

```bash
chmod 400 mykey.pem
ssh -i mykey.pem ubuntu@<EC2_PUBLIC_IP>
```

---

## ✅ Step 4: Install Base Tools

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl wget unzip net-tools htop
```

### Why each tool exists:

| Tool      | Purpose            |
| --------- | ------------------ |
| git       | version control    |
| curl      | API testing        |
| wget      | file download      |
| unzip     | extract files      |
| net-tools | network commands   |
| htop      | process monitoring |

---

## 🎯 Practice Tasks

- Create 3 directories: dev, test, prod  

```
mkdir dev test prod
```
### Why?

Simulates real environment separation:

- dev = development

- test = testing

- prod = production

- SSH reconnect without errors  

- Block and allow ports from security group  



---

# 🐧 PHASE 2: LINUX (REAL DEVOPS TASKS)

## 🔹 File & Directory

```bash
ls -la
cp file1.txt backup.txt
mv file1.txt /tmp/
rm -rf temp*
find / -name "*.log"
```

---

## 🔹 Users & Permissions

```bash
sudo useradd devops
sudo passwd devops
sudo groupadd engineers
sudo usermod -aG engineers devops
chmod 755 script.sh
chown ubuntu:ubuntu file.txt
```

---

## 🔹 Processes

```bash
ps aux
top
htop
kill -9 <PID>
```

---

## 🔹 Disk

```bash
df -h
du -sh *
```

---

## 🔹 Logs

```bash
cd /var/log
tail -f syslog
journalctl -xe
```

---

## 🔹 Networking

```bash
ping google.com
curl ifconfig.me
ss -tulnp
```

---

## 🔹 Bash Script (REAL)

```bash
nano backup.sh

#!/bin/bash
tar -czf backup-$(date +%F).tar.gz /home/ubuntu
```

---

## 🎯 Practice Tasks

- Create script to delete old logs  
- Monitor CPU usage  
- Create auto backup script  

---

# 🔧 PHASE 3: GIT + GITHUB LAB

## Install Git

```bash
sudo apt install git -y
git config --global user.name "yourname"
git config --global user.email "you@example.com"
```

---

## Create Repo

```bash
mkdir microservices-app && cd microservices-app
git init
```

---

## Connect to GitHub

```bash
git remote add origin https://github.com/<username>/devops-lab.git
```

---

## Branching

```bash
git checkout -b feature-login
git branch -m feature-auth
git branch -d old-branch
```

---

## Advanced Git

```bash
git stash
git stash pop
git tag v1.0
git log --oneline
git diff
git reset --hard HEAD~1
git revert HEAD
git cherry-pick <commit>
```

---

## 🎯 Practice Tasks

- Create 2 branches and merge them  
- Create tag v1.0 and push  
- Simulate conflict and resolve  

---

# 🐳 PHASE 4: DOCKER LAB

## Install Docker

```bash
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
```

---

## Dockerfile Example (Node.js)

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

---

## Build & Run

```bash
docker build -t app:v1 .
docker run -d -p 3000:3000 app:v1
```

---

## Volumes

```bash
docker run -d -v /data:/app/data app:v1
```

---

## Docker Compose

```yaml
version: "3"
services:
  app:
    build: .
    ports:
      - "3000:3000"
```

## Run in Background

```bash
docker-compose up -d
```
- -d means detached mode. 
---

## Check Running Containers

```
docker ps
```

## Stop Containers

```
docker compose down
```

This stops and removes containers.

## Most Important Compose Commands

### Start

```
docker compose up
```

### Background Start

```
docker compose up -d
```

### Stop

```
docker compose stop
```

### Remove Everything

```
docker compose down
```

### Restart

```
docker compose restart
```

### View Logs

```
docker compose logs
```

### Live Logs

```
docker compose logs -f
```

### Build Images

```
docker compose build
```

### Pull Images

```
docker compose pull
```

### Check Running Services

```
docker compose ps
```



## 🎯 Practice Tasks

- Run 2 containers  
- Connect containers via network  
- Debug container crash  

---

# 🧩 PHASE 5: MICROSERVICES PROJECT (REAL APP)

## Architecture

- frontend (Node.js)  
- backend (Node.js API)  
- database (MongoDB)  

---

## Backend Example

```javascript
const express = require('express');
const app = express();

app.get('/api', (req,res)=>{
  res.send("Hello from backend");
});

app.listen(4000);
```

---

## Connect Services (Docker Network)

```bash
docker network create devops-net
docker run -d --network devops-net backend
docker run -d --network devops-net frontend
```

---

## 🎯 Practice Tasks

- Add second API endpoint  
- Break service → debug logs  

---

# 🔁 PHASE 6: CI/CD WITH GITHUB ACTIONS

## Create Workflow

```yaml
name: DevOps Pipeline

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Build Docker Image
      run: docker build -t app .

    - name: Push to DockerHub
      run: docker push <username>/app

    - name: Deploy to EC2
      run: ssh ubuntu@<IP> "docker pull <username>/app && docker run -d -p 3000:3000 <username>/app"
```

---

## 🎯 Practice Tasks

- Trigger pipeline on push  
- Break build intentionally  
- Fix pipeline  

---

# 🔐 PHASE 7: SECURITY

## IAM (AWS)

- IAM Role for EC2  
- No hardcoded credentials  

---

## Secrets in GitHub  

### Store Secrets

- SSH key  
- Docker credentials  

---

## Vulnerability Scan (Trivy)

```bash
sudo apt install trivy
trivy image app:v1
```

---

# 📊 PHASE 8: MONITORING

## Install Prometheus

```bash
wget https://github.com/prometheus/prometheus/releases/download/...tar.gz
```

---

## Install Grafana

```bash
sudo apt install grafana -y
sudo systemctl start grafana-server
```

---

## Access Grafana

```
http://<EC2-IP>:3001
```

---

## 🎯 Practice Tasks

- Monitor CPU usage  
- Add dashboard  
- Simulate high load  

---

# 🔥 FINAL REAL-WORLD SCENARIO

You are a DevOps Engineer:

- Developer pushes code  
- Pipeline runs  
- Docker image builds  
- Security scan runs  
- Image pushed  
- EC2 auto-updates container  
- Monitoring shows metrics  

---

# ⚠️ TROUBLESHOOTING (IMPORTANT)

## Docker Issue
```bash
sudo systemctl restart docker
```

## Port Issue
```bash
sudo ss -tulnp
```

## Permission Issue
```bash
sudo chmod -R 777 project/
```

## Pipeline Issue
- Check GitHub Actions logs  
- Verify secrets  

---

# 🎯 FINAL RESULT (WHAT YOU WILL MASTER)

After completing this lab, you will:

- Think like a DevOps Engineer  
- Deploy real microservices  
- Build CI/CD pipelines  
- Debug production issues  
- Work with AWS in real scenarios  

---

# 💡 IMPORTANT (REAL TALK)

Don’t just read this.

👉 Build it step-by-step  
👉 Break things intentionally  
👉 Fix them  

That’s how DevOps engineers are made — not by theory.

---

## 🚀 Best Way For S3 Data Transfer

### 1. Create Bucket In New AWS Account 

_Example:_
- Old bucket: `"old-bucket"`
- New bucket: `"new-bucket"`

### 2. In NEW Account Add Bucket Policy 

- Go to:  `S3 → new-bucket → Permissions → Bucket Policy`

#### Replace IDs and paste:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::OLD_ACCOUNT_ID:root"
      },
      "Action": [
        "s3:PutObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::new-bucket",
        "arn:aws:s3:::new-bucket/*"
      ]
    }
  ]
}
```

### 3. Configure AWS CLI With OLD Account

aws configure --profile old

### 4. Direct Transfer (No Download)
aws s3 sync s3://old-bucket s3://new-bucket --profile old
---