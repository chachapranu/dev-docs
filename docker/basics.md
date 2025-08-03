# 🐳 Docker on WSL2 — Learning Setup & Reference Guide

## 💻 System Context
- **Platform**: WSL2 with Ubuntu 24.04
- **Purpose**: Create containers for learning, experimentation, and development
- **Tools**: Docker, VS Code (integration planned)

---

## 🏷️ Naming Convention Strategy

Use a clean, scalable format to name both **images** and **containers**:

```
learn-[tech]-[topic]-[version]
```

**Examples**:
- `learn-linux-cli-v1`
- `learn-python-flask-v2`

This pattern helps track iterations and keeps things organized.

---

## 📁 Recommended Folder Structure

Organize each experiment in its own subfolder:

```
~/docker-lab/
│
├── docker-basics/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── notes.md
```

Each folder acts as a self-contained workspace with documentation and build assets.

---

## 📦 Starter Dockerfile (Ubuntu 24.04 CLI Environment)

```dockerfile
FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl git vim htop net-tools iputils-ping build-essential \
    python3 python3-pip && apt-get clean

WORKDIR /workspace
CMD ["bash"]
```

This provides a learning-friendly CLI environment with essential tools pre-installed.

---

## 🚫 `.dockerignore` Best Practices

Keep builds fast and clean by ignoring clutter:

```
# Common build artifacts and cache
node_modules
__pycache__/
*.pyc
*.log

# Version control
.git/
.gitignore

# Editor folders
.vscode/
.idea/

# OS-specific files
.DS_Store
Thumbs.db

# Sensitive or build output
.env
dist/
build/
```

---

## 🔨 Building the Image

Run this command from **one level above** your Dockerfile folder:

```bash
cd ~/docker-lab/
docker build -t learn-linux-cli-v1 ./docker-basics
```

- `-t` assigns a tag to the image (`learn-linux-cli-v1`)
- `./docker-basics` is the build context folder containing the Dockerfile

---

## 🚀 Running the Container

After building, you can launch the container from **anywhere**:

```bash
docker run -it --name learn-linux-cli-v1 learn-linux-cli-v1
```

### 🤔 Why Two Names?

| Component | Meaning |
|----------|---------|
| `--name learn-linux-cli-v1` | This names the **container instance** you're starting |
| `learn-linux-cli-v1` (last part) | Refers to the **Docker image tag** you built earlier |

They can match or differ—it’s up to your organization preference.

### ✨ Disposable Alternative

Use `--rm` to auto-delete the container after use:

```bash
docker run -it --rm learn-linux-cli-v1
```

