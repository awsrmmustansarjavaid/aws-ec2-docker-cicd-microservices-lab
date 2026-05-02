**🚀 COMPLETE AWS DEVOPS LAB (FULL STEP-BY-STEP GUIDE)**

**🧱 PHASE 1: AWS EC2 SETUP (FOUNDATION)**

**✅ STEP 1: Launch EC2 Instance (AWS Console)**

Go to Amazon Web Services → EC2 → Launch Instance

**Settings:**

-   Name: devops-lab-server
-   OS: Ubuntu 22.04 LTS
-   Instance type: t2.micro (free tier)

**Why this matters:**

-   EC2 = your real Linux server in cloud
-   Ubuntu = most widely used DevOps OS
-   t2.micro = free lab environment

**🔐 STEP 2: Create Key Pair**

Download .pem file

**Why?**

-   This is your SSH authentication key
-   Without it → you CANNOT access server

**🔥 STEP 3: Security Group Setup**

Open ports:

| Port      | Purpose                |
| --------- | ---------------------- |
| 22        | SSH access             |
| 80        | HTTP web traffic       |
| 443       | HTTPS secure traffic   |
| 3000–5000 | Apps (Docker services) |
| 9090      | Prometheus             |
| 3001      | Grafana                |


**Why this is critical:**

Security Group = firewall of AWS

👉 It controls WHO can access your server

**💻 STEP 4: Connect to EC2 via SSH**

```
chmod 400 mykey.pem
```

**Why?**

-   Restricts file permission
-   SSH refuses insecure keys

```
ssh -i mykey.pem ubuntu@<EC2\_PUBLIC\_IP>
```
**Why?**

-   Connects your laptop → remote AWS server
-   \-i means identity file (your private key)

**⚙️ STEP 5: Install Base Tools**

```
sudo apt update && sudo apt upgrade -y
```

**Why?**

-   Updates package list
-   Installs latest security patches

```
sudo apt install -y git curl wget unzip net-tools htop
```

**Why each tool exists:**

| Tool      | Purpose            |
| --------- | ------------------ |
| git       | version control    |
| curl      | API testing        |
| wget      | file download      |
| unzip     | extract files      |
| net-tools | network commands   |
| htop      | process monitoring |


**🎯 PRACTICE TASKS**

```
mkdir dev test prod
```

**Why?**

Simulates real environment separation:

-   dev = development
-   test = testing
-   prod = production

**🐧 PHASE 2: LINUX MASTERING (DEVOPS CORE)**

**📂 FILE SYSTEM COMMANDS**

```
ls -la
```

**Why?**

Shows ALL files including hidden ones + permissions

```
cp file1.txt backup.txt
```

Why:

-   Copy file for backup safety

```
mv file1.txt /tmp/
```

Why:

-   Move file to temporary storage

```
rm -rf temp\*
```

⚠️ WARNING COMMAND

Why:

-   Deletes unwanted files/folders recursively

```
find / -name "\*.log"
```

Why:

-   Search system logs for debugging

**👤 USERS & PERMISSIONS**

```
sudo useradd devops
```

Why:

-   Creates new Linux user

```
sudo passwd devops
```

Why:

-   Assign password to user

```
sudo groupadd engineers
```

Why:

-   Group multiple users

```
sudo usermod -aG engineers devops
```

Why:

-   Adds user to group

```
chmod 755 script.sh
```

Why:

-   Controls file permissions:
    -   7 = full access
    -   5 = read + execute

```
chown ubuntu:ubuntu file.txt
```

Why:

-   Changes ownership

**⚙️ PROCESS MANAGEMENT**

```
ps aux
```

Why:

-   Shows all running processes

```
top  
htop
```

Why:

-   Real-time CPU/memory monitoring

```
kill -9 <PID>
```

Why:

-   Force stop crashed process

**💽 DISK USAGE**

```
df -h
```

Why:

-   Shows disk space usage

```
du -sh \*
```

Why:

-   Shows folder sizes

**📜 LOGS (VERY IMPORTANT IN DEVOPS)**

```
cd /var/log
```

Why:

-   System logs location

```
tail -f syslog
```

Why:

-   Live log monitoring

```
journalctl -xe
```
Why:

-   System service debugging

**🌐 NETWORKING**

```
ping google.com
```

Why:

-   Check internet connectivity

```
curl ifconfig.me
```

Why:

-   Get public IP

```
ss -tulnp
```

Why:

-   Show open ports (very important for debugging)

**🧠 BASH SCRIPT**

```
nano backup.sh
```

**Script:**

```
#!/bin/bash  
tar -czf backup-$(date +%F).tar.gz /home/ubuntu
```

**Why?**

-   Automates backups
-   $(date) adds timestamp
-   .tar.gz compresses files

**🔧 PHASE 3: GIT + GITHUB (VERSION CONTROL)**

Install Git:

```
sudo apt install git -y
```

Why:

-   Enables version control system

```
git config --global user.name "yourname"  
git config --global user.email "you@example.com"
```

Why:

-   Identifies your commits

**CREATE PROJECT**

```
mkdir microservices-app && cd microservices-app  
git init
```

Why:

-   Initializes Git repository

**CONNECT TO GitHub**

```
git remote add origin https://github.com/<username>/devops-lab.git
```

Why:

-   Connect local project → GitHub cloud repo

**BRANCHING**

```
git checkout -b feature-login
```

Why:

-   Creates isolated development branch

```
git branch -m feature-auth
```

Why:

-   Renames branch

```
git branch -d old-branch
```

Why:

-   Deletes unnecessary branch

**ADVANCED GIT**

```
git stash
```

Why:

-   Temporarily saves work

```
git stash pop
```

Why:

-   Restores saved work

```
git reset --hard HEAD~1
```

Why:

-   Undo last commit completely

```
git revert HEAD
```

Why:

-   Safe undo (used in production)

**🐳 PHASE 4: DOCKER (CONTAINERS)**

Install Docker

```
sudo apt install docker.io -y
```

Why:

-   Installs container engine

```
sudo systemctl start docker  
sudo systemctl enable docker
```

Why:

-   Starts Docker service automatically

```
sudo usermod -aG docker $USER
```

Why:

-   Allows running Docker without sudo

**DOCKER IMAGE**

```
FROM node:18  
WORKDIR /app  
COPY . .  
RUN npm install  
CMD \["node", "app.js"\]
```

Why:

-   Defines how application runs inside container

**BUILD IMAGE**

```
docker build -t app:v1 .
```

Why:

-   Converts code → container image

**RUN CONTAINER**

```
docker run -d -p 3000:3000 app:v1
```

Why:

-   Runs app in background
-   Maps host port → container port

**🧩 PHASE 5: MICROSERVICES**

You build:

-   Frontend
-   Backend API
-   Database

Why:

-   Real companies never use single app
-   They use distributed systems

**NETWORKING BETWEEN SERVICES**

```
docker network create devops-net
```

Why:

-   Creates internal communication layer

**🔁 PHASE 6: CI/CD (AUTOMATION)**

Using GitHub Actions

Workflow:

```
on: push
```

Why:

-   Triggers pipeline automatically

Steps:

1.  Checkout code
2.  Build Docker image
3.  Push image
4.  Deploy to EC2

Why CI/CD matters:

-   Removes manual deployment
-   Reduces human errors
-   Enables fast delivery

**🔐 PHASE 7: SECURITY**

**IAM**

Why:

-   Controls AWS access safely

**Secrets**

-   Never store passwords in code
-   Use GitHub Secrets

**Scan image**

trivy image app:v1

Why:

-   Finds vulnerabilities in container

**📊 PHASE 8: MONITORING**

Install:

Prometheus  
Grafana

Why:

-   Prometheus collects metrics
-   Grafana visualizes them

**FLOW**

EC2 → Prometheus → Grafana → Dashboard

**🚨 FINAL REAL FLOW (COMPLETE SYSTEM)**

```
Developer  
↓  
GitHub  
↓  
GitHub Actions  
↓  
Docker Build  
↓  
Docker Hub  
↓  
EC2 Server  
↓  
Containers Running  
↓  
User Access  
↓  
Prometheus Monitoring  
↓  
Grafana Dashboard
```

**🧠 FINAL TRUTH (IMPORTANT)**

If you complete this lab properly:

👉 You will NOT be beginner anymore  
👉 You will think like real DevOps engineer  
👉 You will understand production systems