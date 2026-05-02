### AWS DEVOPS Lab # 1  

# 🚀 End-to-End AWS DevOps Microservices Lab  

> ## (EC2 + Docker + CI/CD + Monitoring)

---

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

Install Prometheus & Grafana:

Monitor:

- CPU usage  
- Memory usage  
- Container health  
- System overload  

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

