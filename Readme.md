docker run my-first-image

# 🚀 Docker on EC2: Modern Quickstart Guide

This guide helps you set up Docker on an Amazon EC2 instance and build your first Docker image. All commands are grouped for easy copy-paste. No commands have been removed.

---

## 1. Install Docker on EC2

**Connect to your EC2 instance via SSH, then run the commands for your OS:**

### Amazon Linux 2023 / Amazon Linux 2

```bash
# Update the system
sudo dnf update -y
# Install Docker
sudo dnf install -y docker
# Start Docker service
sudo systemctl start docker
# Enable Docker to start on boot
sudo systemctl enable docker
```

### Ubuntu

```bash
# Update package list
sudo apt-get update
# Install Docker
sudo apt-get install -y docker.io
# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker


Download the binary:

Bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
Make it executable:

Bash
sudo chmod +x /usr/local/bin/docker-compose
```

---

## 2. Configure Docker Permissions

By default, you need `sudo` for every Docker command. To run Docker as a standard user (e.g., `ec2-user` or `ubuntu`):

```bash
# Add current user to the docker group
sudo usermod -aG docker $USER
# Apply the group change immediately (or log out and back in)
newgrp docker
# Test Docker access
docker ps
```

---

## 3. Create and Build a Docker Image

### A. Create a project directory

```bash
mkdir my-app && cd my-app
```

### B. Create a simple Dockerfile

Create a file named `Dockerfile` with the following content:

```dockerfile
# Use a light base image
FROM alpine
# Execute a simple command
CMD ["echo", "Hello from Docker on EC2!"]
```

### C. Build the Docker image

```bash
# Build the image (don't forget the dot at the end)
docker build -t my-first-image .
```

---

## 4. Run Your Container

```bash
docker run my-first-image
# Output: Hello from Docker on EC2!
```

---

## 🛠️ Pro Tips for EC2

- **Storage:** If you plan to build many large images, ensure your EC2 instance has enough EBS storage (the default 8GB fills up quickly with Docker layers).
- **Security Groups:** If your Docker container runs a web server (e.g., on port 80), open that port in your AWS EC2 Security Group settings.

---

_Need a more complex Dockerfile for Python, Node.js, or Java? Let me know!_
