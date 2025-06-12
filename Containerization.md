# 🐳 Containerization in Linux

Containerization is the process of packaging and running applications in isolated environments called containers. Containers offer consistent, lightweight environments that work uniformly across development, testing, and production systems.

---

## 🚀 Benefits of Containerization

* **Portability**: Runs the same across any environment.
* **Efficiency**: Shares the host's kernel; lightweight compared to VMs.
* **Security**: Isolated environments reduce system-level risks.
* **Scalability**: Run multiple containers simultaneously.
* **Configurability**: Tailor to specific application needs.

Imagine each app is a band, and containers are self-contained "stage pods" with everything needed. Instead of building a whole new stage (VM) for each, you place a pod on a shared stage (host). Efficient and reusable.

---

## 🐋 Docker: The Leading Container Platform

Docker is an open-source platform that simplifies container creation, deployment, and management.

### 📦 Docker Installation (Ubuntu)

```bash
#!/bin/bash
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker htb-student
```

✅ Log out and back in to apply group changes.

### ✅ Verify Docker

```bash
docker run hello-world
```

---

## 📁 Dockerfile Example: File Transfer Container

```Dockerfile
FROM ubuntu:22.04
RUN apt-get update && \
    apt-get install -y apache2 openssh-server && \
    rm -rf /var/lib/apt/lists/*
RUN useradd -m docker-user && \
    echo "docker-user:password" | chpasswd
RUN chown -R docker-user:docker-user /var/www/html /var/run/apache2 /var/log/apache2 /var/lock/apache2 && \
    usermod -aG sudo docker-user && \
    echo "docker-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
EXPOSE 22 80
CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
```

### 🔧 Build Image

```bash
docker build -t FS_docker .
```

### 🛠️ Run Container

```bash
docker run -p 8022:22 -p 8080:80 -d FS_docker
```

---

## 🛠️ Docker Management Commands

| Command              | Description             |
| -------------------- | ----------------------- |
| `docker ps`          | List running containers |
| `docker stop <id>`   | Stop container          |
| `docker start <id>`  | Start container         |
| `docker rm <id>`     | Remove container        |
| `docker rmi <image>` | Remove image            |
| `docker logs <id>`   | View logs               |

Changes to running containers aren't persistent. To keep them, create a new image via Dockerfile.

---

## 🧱 Linux Containers (LXC)

LXC offers system-level virtualization, creating containers that resemble lightweight VMs.

### 🔧 Install LXC

```bash
sudo apt-get install lxc lxc-utils -y
```

### 🆕 Create Container

```bash
sudo lxc-create -n linuxcontainer -t ubuntu
```

### 🔎 LXC Management Commands

| Command                           | Description         |
| --------------------------------- | ------------------- |
| `lxc-ls`                          | List containers     |
| `lxc-start -n <name>`             | Start container     |
| `lxc-stop -n <name>`              | Stop container      |
| `lxc-attach -n <name>`            | Attach to container |
| `lxc-config -n <name> -s network` | Configure network   |

### 🔐 Secure LXC

Create resource-limiting config:

```bash
sudo vim /usr/share/lxc/config/linuxcontainer.conf
```

Add:

```txt
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
```

Restart LXC:

```bash
sudo systemctl restart lxc.service
```

---

## 🎯 Use Cases in Penetration Testing

* Build custom containers with specific vulnerabilities.
* Simulate attack surfaces without affecting host system.
* Transfer files with embedded services like Apache or SSH.

---

## 🧪 Practice Tasks

1. Install and configure LXC.
2. Build a Dockerfile for a web server.
3. Limit container resources.
4. SSH into your containers.
5. Host files inside a Docker container.

---

📁 This document is part of my Linux Fundamentals and Offensive Security Notes. More walkthroughs and resources available in my GitHub.

🔗 Happy Hacking!
