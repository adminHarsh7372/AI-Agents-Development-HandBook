# 🛠️ Building Docker Images

Creating your own Docker image gives you full control over the environment and app configuration.

Let’s dive into how to build custom images using `Dockerfile`.

---

## 📄 Step 1: Create a `Dockerfile`

A `Dockerfile` is a plain text file that contains instructions to build an image.

```Dockerfile
# Use a base image
FROM node:20

# Set working directory
WORKDIR /app

# Copy files into the image
COPY . .

# Install dependencies
RUN npm install

# Expose the app port
EXPOSE 3000

# Command to run the app
CMD ["npm", "start"]
```

Save this file as `Dockerfile` (no extension).

---

## ⚙️ Step 2: Build the Image

```bash
docker build -t my-node-app .
```

* `-t`: Tag the image (give it a name)
* `.`: Location of Dockerfile

Once built, verify with:

```bash
docker images
```

---

## 🚀 Step 3: Run the Custom Image

```bash
docker run -p 3000:3000 my-node-app
```

Your Node.js app will be live on `http://localhost:3000`

---

## 🧠 Best Practices

* Use smaller base images: `node:20-alpine`, `python:3.10-slim`
* Group commands smartly to optimize layers
* Use `.dockerignore` to exclude unnecessary files (like `node_modules`, `.git`, etc)

Example `.dockerignore`:

```
node_modules
.git
Dockerfile
*.log
```

---

## 💥 Rebuild When Code Changes

If your app files change:

```bash
docker build -t my-node-app .
```

Then re-run the container.

---

## 📦 Multi-Stage Builds (Optional, Advanced)

Use multi-stage to keep final image small:

```Dockerfile
# Stage 1: build
FROM node:20 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2: run
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]
```

---

✅ That’s it! You now know how to build Docker images and run your own containers from scratch.

→ Next: [04_volume-binds.md](04_volume-binds.md)
