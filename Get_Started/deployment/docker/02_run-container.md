# 🐳 Running Docker Containers

Once Docker is installed, the first command you’ll use the most is:

```bash
docker run IMAGE_NAME
```

Let’s break down how to use `docker run` effectively.

---

## 🔹 Basic Usage

```bash
docker run hello-world
```

This pulls and runs the `hello-world` image — perfect to test Docker installation.

---

## 🔹 Run in Interactive Mode

```bash
docker run -it ubuntu bash
```

* `-i`: Interactive
* `-t`: TTY terminal
* `ubuntu`: Image name
* `bash`: Command to run

You’ll land inside an Ubuntu terminal running inside a container.

---

## 🔹 Run in Detached (Background) Mode

```bash
docker run -d nginx
```

* `-d`: Run in background
* Access NGINX by visiting `http://localhost:80` (if exposed)

---

## 🔹 Expose Container Port to Host

```bash
docker run -d -p 8080:80 nginx
```

* Maps `host:8080` to `container:80`
* Open `http://localhost:8080` in your browser

---

## 🔹 Mounting Volumes

### Named volume:

```bash
docker run -d -v mydata:/usr/share/nginx/html nginx
```

### Bind mount (local folder):

```bash
docker run -d -v $(pwd)/site:/usr/share/nginx/html nginx
```

* This way you can sync files between host and container.

---

## 🔹 Passing Environment Variables

```bash
docker run -d -e MY_NAME=nihal ubuntu env
```

Use `-e` to pass environment variables inside the container.

---

## 🔹 Give Your Container a Name

```bash
docker run -d --name mynginx nginx
```

Now you can stop/start by name:

```bash
docker stop mynginx
docker start mynginx
```

---

## 🔹 Auto Restart on Reboot

```bash
docker run -d --restart always nginx
```

Useful for production — container restarts if host reboots.

---

## ✅ Summary Cheatsheet

| Flag        | Use                          |
| ----------- | ---------------------------- |
| `-d`        | Run in background            |
| `-p`        | Port mapping                 |
| `-v`        | Volume mounting              |
| `-e`        | Set environment variable     |
| `--name`    | Name your container          |
| `--restart` | Restart policy (e.g. always) |
| `-it`       | Interactive terminal         |

---

### 🧠 Tip: List All Running Containers

```bash
docker ps
```

To list all containers (even stopped ones):

```bash
docker ps -a
```

---

🎉 That’s it! You now know how to run, manage, and control containers like a pro.

→ Next: [03_build-images.md](03_build-images.md)
