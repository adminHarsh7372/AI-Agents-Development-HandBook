# 📦 Volume Binds in Docker

Docker volumes help persist data and share files between your container and your local system. In development, they are super helpful for live reloading and debugging.

Let’s understand volume binds using examples.

---

## 🔄 What Is a Volume Bind?

A bind mount maps a file or directory on the host to a path in the container.

```bash
docker run -v /host/path:/container/path image-name
```

* `/host/path`: path on your system
* `/container/path`: path inside the container

---

## 🧪 Example: Live Code Mounting

```bash
docker run -p 3000:3000 \
  -v $(pwd):/app \
  -w /app \
  node:20 \
  sh -c "npm install && npm start"
```

What this does:

* Maps current folder to `/app` in container
* Installs dependencies and starts the app
* Reflects file changes live without rebuilding image

---

## 📁 Named Volumes vs Bind Mounts

| Feature     | Bind Mounts           | Named Volumes        |
| ----------- | --------------------- | -------------------- |
| File Source | Your system           | Managed by Docker    |
| Use Case    | Local dev             | Persistent data (DB) |
| Flexibility | High (manual control) | Auto-managed         |
| Performance | Slightly slower (dev) | Faster (prod)        |

---

## 🧹 Example: Named Volume

```bash
docker volume create mydata

docker run -d \
  -v mydata:/data \
  --name my-container \
  ubuntu
```

---

## 🛑 Removing Volumes

To remove anonymous volumes:

```bash
docker container prune
```

To remove named volume:

```bash
docker volume rm mydata
```

---

## 📌 .dockerignore Tip

When using bind mounts, make sure `.dockerignore` exists to avoid syncing unwanted files.

Example:

```
node_modules
.env
*.log
```

---

✅ That’s all for volume binds! You now know how to mount your code into containers and manage persistent data.

→ Next: [05_cloud-ready.md](05_cloud-ready.md)
