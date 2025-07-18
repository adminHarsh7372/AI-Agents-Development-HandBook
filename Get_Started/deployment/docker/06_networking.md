# 🌐 Docker Networking Basics

In real-world applications, containers need to talk to each other — databases, APIs, or web frontends. Let’s explore how Docker handles networking.

---

## 🔌 1. Types of Docker Networks

### ✅ Bridge (default)

Used for communication between containers on the same host.

```bash
docker network ls
```

You’ll see a default `bridge` network.

---

### 🌍 Host

Shares the host’s network stack.

```bash
docker run --network host nginx
```

Use this for performance-sensitive apps (not available on Mac/Windows).

---

### 🔒 None

Disables networking for the container.

```bash
docker run --network none your-image
```

---

## 🛠️ 2. Custom Bridge Networks

Recommended for multi-container setups.

```bash
docker network create ai-agent-net
```

Then attach containers:

```bash
docker run -d --name db --network ai-agent-net postgres

docker run -d --name backend --network ai-agent-net your-backend
```

Now `backend` can talk to `db` using the name `db` as hostname.

---

## 🧪 3. Test Container Connectivity

```bash
docker exec -it backend ping db
```

Output:

```bash
PING db (172.18.0.2): 56 data bytes
```

---

## 🧱 4. Exposing Ports

```bash
docker run -p 8080:3000 your-app
```

Format: `hostPort:containerPort`

Access app at `http://localhost:8080`

---

## 🔐 5. Real Use: Backend + DB

```bash
docker network create mynet

docker run -d --name mongo --network mynet mongo

docker run -d --name app --network mynet your-node-app
```

Inside your app config:

```env
DB_HOST=mongo
DB_PORT=27017
```

---

## 🔄 6. Docker Compose (Preferred)

```yaml
services:
  mongo:
    image: mongo
  backend:
    image: your-backend
    depends_on:
      - mongo
```

All services are automatically connected on a single network.

---

## ✅ Summary

* Use custom bridge networks for multi-container apps
* Containers on the same network can resolve each other by name
* Use `docker-compose` for easier networking and scaling

→ Next up: Learn how to **secure containers**, manage **Docker volumes**, or deploy multi-container stacks.
