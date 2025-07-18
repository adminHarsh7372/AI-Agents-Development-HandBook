# ☁️ Using Docker Images in the Cloud

Once you've published your Docker image, here’s how to run it on various cloud platforms.

---

## 🚀 1. AWS EC2 (Basic Server)

SSH into your EC2 server and run:

```bash
sudo apt update && sudo apt install docker.io -y

sudo docker pull yourname/agent-app:latest

sudo docker run -d -p 3000:3000 yourname/agent-app:latest
```

💡 Use security group to open port 3000.

---

## 🔁 2. Railway / Render / Zeabur

These platforms support auto-deploy from GitHub or Dockerfile:

* Connect GitHub repo
* Set Dockerfile as the entry
* Define ports, env vars
* Done!

Zero server management.

---

## ⚓ 3. Docker on GCP VM / Azure VM

Same as EC2:

```bash
# On your VM:
docker pull yourname/agent-app:latest
docker run -d -p 3000:3000 yourname/agent-app:latest
```

Just make sure firewall rules allow external access.

---

## 🐳 4. Use in Kubernetes (GKE, AKS, EKS)

1. Create a deployment YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: agent-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: agent
  template:
    metadata:
      labels:
        app: agent
    spec:
      containers:
      - name: agent
        image: yourname/agent-app:latest
        ports:
        - containerPort: 3000
```

2. Apply to cluster:

```bash
kubectl apply -f deployment.yaml
```

3. Expose it with a service or ingress.

---

## 🔐 5. Environment Variables

Use `-e` flag in Docker:

```bash
docker run -e API_KEY=1234 -p 3000:3000 yourname/agent-app
```

Or inject them via cloud provider’s secret manager / UI.

---

## 📦 6. Volume Mounts for Persistent Data

```bash
docker run -v /host/logs:/app/logs yourname/agent-app
```

Use this if your container generates data.

---

## ✅ Summary

* Pull and run anywhere with `docker run`
* Use managed cloud services for quick deployment
* Kubernetes for scaling and orchestration
* Always handle env vars + volumes securely

