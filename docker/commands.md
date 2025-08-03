# Docker Common Commands

## Installation

### On Ubuntu

```bash
sudo apt update
sudo apt install \
    ca-certificates \
    curl \
    gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Installation

```bash
docker --version
sudo systemctl status docker
```

## Maintenance

### Start/Stop Docker

```bash
sudo systemctl start docker
sudo systemctl stop docker
sudo systemctl restart docker
```

### Enable Docker on Boot

```bash
sudo systemctl enable docker
```

### Check Docker Status

```bash
sudo systemctl status docker
```

### Remove Unused Data

```bash
docker system prune
```

### List Running Containers

```bash
docker ps
```

### List All Containers

```bash
docker ps -a
```

### Remove a Container

```bash
docker rm <container_id>
```

### Remove an Image

```bash
docker rmi <image_id>
```

---

Add more sections as needed for your workflow!