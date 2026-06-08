# Docker Installation Guide for Ubuntu (CLI + GUI)

> Installs Docker Engine (CLI), Docker Desktop (GUI), Docker permissions, and Docker Desktop auto-start on a fresh Linux based OS i.e: Ubuntu system.


---

## 1. Update Ubuntu

Open Terminal with `Ctrl + Alt + T`, then run:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install Required Packages

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

---

## 3. Create Docker Keyring Folder

```bash
sudo mkdir -p /etc/apt/keyrings
```

---

## 4. Add Docker Official GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.asc
```

Then set read permissions:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

---

## 5. Add Docker Repository

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## 6. Update Package List

```bash
sudo apt update
```

---

## 7. Install Docker Engine

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 8. Verify Docker Installation

```bash
docker --version
```

Expected output:

```
Docker version xx.x.x
```

---

## 9. Start Docker Service

Enable Docker to start on boot:

```bash
sudo systemctl enable docker
```

Start the service now:

```bash
sudo systemctl start docker
```

Check service status:

```bash
sudo systemctl status docker
```

Expected output includes:

```
active (running)
```

---

## 10. Create Docker Group

```bash
sudo groupadd docker
```

> If you see `group already exists` — ignore it and continue.

---

## 11. Add User to Docker Group

```bash
sudo usermod -aG docker $USER
```

---

## 12. Refresh Group Permissions

```bash
newgrp docker
```

---

## 13. Test Docker CLI

```bash
docker run hello-world
```

A successful installation will print:

```
Hello from Docker!
```

✅ **Docker CLI installation is complete.**

---

## 14. Download Docker Desktop

**Option A — Browser:**  
Visit the [Docker Desktop Linux download page](https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb)

**Option B — Terminal:**

```bash
wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb
```

---

## 15. Install Docker Desktop

If downloaded via browser, navigate to the Downloads folder first:

```bash
cd ~/Downloads
```

Install the package:

```bash
sudo apt install ./docker-desktop-amd64.deb
```

Enter `Y` when prompted to confirm.

---

## 16. Start Docker Desktop

Start the service:

```bash
systemctl --user start docker-desktop
```

Enable auto-start on login:

```bash
systemctl --user enable docker-desktop
```

---

## 17. Open Docker GUI

1. Open the Activities menu
2. Search for **Docker Desktop**
3. Launch the app
4. Accept the terms on first launch

---

## 18. Verify Docker Desktop

```bash
docker context ls
```

You should see `desktop-linux` listed in the output.

---

## 19. Useful Beginner Commands

| Command | Description |
|---|---|
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (including stopped) |
| `docker images` | List downloaded images |
| `docker run -it ubuntu bash` | Run an interactive Ubuntu container |

**Exit a running container:**

```bash
exit
```

---

## Final Result

| Component | Status |
|---|---|
| Docker Engine (CLI) | ✅ Installed |
| Docker Desktop (GUI) | ✅ Installed |
| Docker permissions | ✅ Configured |
| Docker auto-start | ✅ Enabled |

---

All Done.. 😊
