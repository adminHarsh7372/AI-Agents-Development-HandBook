# Install Docker

To run your AI agents inside containers, you’ll need Docker installed on your system. Follow these simple steps to get started.

---

## 💻 Step 1: Download Docker

Go to the official Docker page based on your OS:

- [Docker for Windows](https://docs.docker.com/desktop/install/windows-install/)
- [Docker for macOS](https://docs.docker.com/desktop/install/mac-install/)
- [Docker for Linux (Ubuntu)](https://docs.docker.com/engine/install/ubuntu/)

> Make sure to download **Docker Desktop** for Windows/macOS  
> On Linux, you'll install Docker Engine directly

---

## 🧰 Step 2: Install Docker

### ✅ For Windows/macOS:
1. Download the `.exe` or `.dmg` file
2. Follow the on-screen installer
3. After installation, restart your machine
4. Open Docker Desktop to verify installation

### 🐧 For Ubuntu:
Run the following in terminal:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```
>*Then check Docker version:*
```bash
docker --version
```
## 👤 Step 3: Run Docker Without sudo (Linux only)
```bash
sudo usermod -aG docker $USER
newgrp docker
```
This lets you run Docker without needing sudo every time.

## ✅ Step 4: Test Your Docker Installation
Run the hello-world container to test:

```bash
docker run hello-world
```
If everything is working, you’ll see a success message.