# f1tenth-gym

A repository for the f1tenth gym environment.

## Table of contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Windows (WSL) setup](#windows-wsl-setup)
- [Ubuntu setup](#ubuntu-setup)
- [Cloning & opening in VS Code](#cloning--opening-in-vs-code)
- [Devcontainer](#devcontainer)
- [Troubleshooting](#troubleshooting)

## Overview
This repo contains code and configuration for running the f1tenth simulation environment in a development container.

## Prerequisites
- Windows 10/11 (or Linux/macOS)
- WSL2 for Windows users
- Visual Studio Code with the "Remote - WSL" and "Remote - Containers" extensions (if using devcontainers)
- Git

## Windows (WSL) setup
1. Install WSL and the Ubuntu distribution:
   - Open PowerShell as Administrator and run:
     ```
     wsl --install -d Ubuntu-24.04
     ```
2. Launch the Ubuntu app from the Windows Start menu (search "Ubuntu").

## Ubuntu setup
1. Install Docker and the Dev-Containers extension in VSCode.

2. Add Docker's official GPG key:
   ```
   sudo apt update
   sudo apt install ca-certificates curl
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc
   ```

3. Add the repository to Apt sources:
   ```
   sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
   Types: deb
   URIs: https://download.docker.com/linux/ubuntu
   Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
   Components: stable
   Signed-By: /etc/apt/keyrings/docker.asc
   EOF

   sudo apt update
   ```

4. Install Docker:
   ```
   sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

5. Add your user to the docker group:
   ```
   sudo usermod -aG docker $USER
   newgrp docker
   ```
   **Note:** Reboot after this step to make the changes effective in VSCode.

6. Give display rights to the local machine:
   ```
   xhost local:root
   ```

## Cloning & opening in VS Code
In the Ubuntu shell:
```
git clone --recurse-submodules -j8 https://github.com/ADTeam-dev/f1tenth-gym.git
cd f1tenth-gym
code .
```

## Devcontainer
Rebuild the container from VS Code (Ctrl+Shift+P → "Remote-Containers: Rebuild and Reopen in Container").

After the container is built and opened, start the simulation inside the devcontainer:
```
ros2 launch f1tenth_gym_ros gym_bridge_launch.py
```

## Troubleshooting
- If `code` is not found in WSL, install the "code" CLI from VS Code (Command Palette → "Shell Command: Install 'code' command in PATH") or use the Remote - WSL extension UI.
- Ensure submodules are initialized if cloning without `--recurse-submodules`:
  ```
  git submodule update --init --recursive
  ```

<!-- end of file -->
