# 🧩 Docker: Multi-Container Applications

Modern AI apps often need **multiple services** — like a frontend, backend, and database. Docker lets you manage all of them together efficiently.

Let’s learn how to orchestrate them using basic commands and `docker-compose`.

---

## ⚙️ 1. Why Multi-Container?

Each container should do **one job only**:

* 🔧 API container
* 📦 Database container
* 🌐 Frontend container

This follows the microservice pattern.

---

## 🛠️ 2. Manual Approach (Not Ideal)

```bash
docker network create aiapp-net

docker run -d --name db --network aiapp-net mongo

docker run -d --name backend --network aiapp-net your-api

docker run -d --name ui --network aiapp-net your-frontend
```

Problems:

* Need to manually manage networks, volumes, dependencies
* Hard to scale or replicate

---

## 🧱 3. Preferred: Docker Compose

A single file to define and run multi-container setups.

### `docker-compose.yml`

```yaml
version: '3'
services:
  mongo:
    image: mongo
    ports:
      - "27017:27017"

  backend:
    image: your-api
    depends_on:
      - mongo
    environment:
      - DB_HOST=mongo

  ui:
    image: your-frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
```

---

## 🚀 4. Run the App

```bash
docker-compose up
```

* Automatically creates a shared network
* All services start in dependency order

---

## 🧹 5. Clean Up

```bash
docker-compose down
```

---

## 🔄 6. Rebuild If Needed

```bash
docker-compose up --build
```

For dev mode with logs:

```bash
docker-compose up --build --remove-orphans
```

---

## ✅ Best Practices

* Isolate responsibilities: 1 job = 1 container
* Use `.env` for environment variables
* Use volume mounts for data persistence
* Compose is preferred over manually managing containers

---

## 📦 Real Example: AI Agent + MongoDB

```yaml
services:
  mongo:
    image: mongo

  agent:
    build: ./agent
    environment:
      - DB_HOST=mongo
```

→ `agent` connects directly to `mongo` inside the network.

---

## 🔚 Summary

Use Docker Compose to:

* Deploy multi-service stacks
* Maintain clean architecture
* Reproduce setups easily across dev, staging, and production


