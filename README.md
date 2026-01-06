# f1tenth-gym

A repository for the f1tenth gym environment.

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
3. In the Ubuntu shell, clone the repository:
   ```
   git clone --recurse-submodules -j8 https://github.com/ADTeam-dev/f1tenth-gym.git
   cd f1tenth-gym
   ```
4. Open the project in VS Code:
   ```
   code .
   ```

## Devcontainer
If you plan to use the devcontainer, edit `.devcontainer/devcontainer.json` to match your username and the path where you cloned the repo, then rebuild the container from VS Code.

## Troubleshooting
- If `code` is not found in WSL, install the "code" CLI from VS Code (Command Palette → "Shell Command: Install 'code' command in PATH") or use the Remote - WSL extension UI.
- Ensure submodules are initialized if cloning without `--recurse-submodules`:
  ```
  git submodule update --init --recursive
  ```

<!-- end of file -->
