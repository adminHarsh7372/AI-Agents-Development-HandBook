# ⚙️ Flowise Setup Guide

Setting up Flowise is simple, whether you're working locally, on an EC2 instance, or preparing it for production. Follow the steps below to get started.

---

## ✅ 1. Install Flowise Locally (No Docker)

This is the quickest way to get started for testing or playing around.

### Prerequisites
- Node.js ≥ 18
- npm (comes with Node)
- Git (optional)

### Installation
```bash
npm install -g flowise
```
### Run
```bash
npx flowise start
```
>That’s it! It will install dependencies and launch the Flowise dashboard at: http://localhost:3000

---
### 🐳 2. Run Flowise with Docker

If you prefer isolation or want to deploy Flowise to a server, you can use docker:

>**Make sure you have Docker and Docker compose is installed**

- Pull the Docker image
```bash
docker pull flowiseai/flowise
```
- b. Run it
```bash
docker run -d -p 3000:3000 \
  -v ~/.flowise:/root/.flowise \
  flowiseai/flowise
```
>🧠 You can now visit http://localhost:3000 in your browser

---
### ☁️ 3. Run on EC2 or VPS (Recommanded)

- Launch an EC2 (t3.medium ) with Ubuntu
- SSH into the instance
- Install Docker + Git
- Run these command 
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install docker
sudo apt install docker-compose
sudo apt install git -y
```
- Now copy the Flowise repo and go to the Flowise docker directory:
```bash
git clone https://github.com/FlowiseAI/Flowise.git
cd Flowise && cd docker
```
- Create a .env file and write
```bash
touch .env
vi .env
```
```text
PORT=3000
DATABASE_PATH=/root/.flowise
APIKEY_PATH=/root/.flowise
SECRETKEY_PATH=/root/.flowise
LOG_PATH=/root/.flowise/logs
```
- *Run Docker compose*
```bash
docker-compose up -d
```
----

#### ⭕ IMPORTANT
- Don’t forget to open port 3000 in your EC2 Security Group:

    - Go to EC2 → Security Groups
    - Edit Inbound Rules
    - Add a new TCP rule for port 3000, open to 0.0.0.0/0 (for public access)
---

*Now you can access the flowise on http:// your instance public ip no:3000*
>*write http not https, otherwise its server issue*