# 📤 Docker Image Publishing

Once your image is production-ready, push it to a registry so others (or your cloud servers) can pull it and run instantly.

---

## 🏷️ 1. Tag Your Image

A tag points to a specific image version:

```bash
docker build -t yourname/agent-app:latest .
docker tag agent-app yourname/agent-app:v1.0.0
```

---

## 🐳 2. Push to Docker Hub

1. Log in:

```bash
docker login
```

2. Push:

```bash
docker push yourname/agent-app:latest
```

✅ Public by default, private if you’ve upgraded your account.

---

## 🏢 3. Push to GitHub Container Registry

1. Login:

```bash
echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin
```

2. Tag and push:

```bash
docker tag agent-app ghcr.io/yourusername/agent-app:latest

docker push ghcr.io/yourusername/agent-app:latest
```

💡 Great for GitHub CI/CD pipelines.

---

## 🔐 4. Private Registries (Optional)

You can use AWS ECR, GCP GCR/Artifact Registry, or Azure ACR.

### Example: AWS ECR

```bash
aws ecr get-login-password | docker login --username AWS --password-stdin [account_id].dkr.ecr.[region].amazonaws.com

docker tag agent-app [account_id].dkr.ecr.[region].amazonaws.com/agent-app:latest

docker push [account_id].dkr.ecr.[region].amazonaws.com/agent-app:latest
```

---

## 🧪 5. Versioning Tips

Always tag your builds clearly:

* `:v1`, `:v1.0`, `:v1.0.2`
* Also push `:latest` for convenience

Avoid overwriting the same version tag!

---

## ✅ Summary

* Use semantic versioning
* Push to Docker Hub for public open-source
* Use GHCR or cloud registries for private/CI use
* Tag everything properly


