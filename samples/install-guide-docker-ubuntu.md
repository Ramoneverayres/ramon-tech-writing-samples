# Install Home Assistant Container on Ubuntu (Docker)

Install and run Home Assistant Container on Ubuntu using Docker. This method is lightweight and easy to revert.

## Prerequisites
- Ubuntu 22.04 LTS (or later) with a user in the `sudoers` group.
- Internet connectivity and at least 2 GB RAM.
- Terminal access.

## Steps

### 1) Update the system
```bash
sudo apt update && sudo apt upgrade -y
```

### 2) Install Docker Engine
```bash
sudo apt install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   $(. /etc/os-release && echo $VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
# Log out/in to apply group membership
```

### 3) Create persistent config directory
```bash
mkdir -p ~/ha-config
```

### 4) Run Home Assistant container
```bash
docker run -d   --name homeassistant   --restart=unless-stopped   -e TZ=Europe/London   -v ~/ha-config:/config   --network=host   ghcr.io/home-assistant/home-assistant:stable
```

> Note: `--network=host` simplifies discovery on a single-host setup.

## Validation
- Open a browser and navigate to `http://<your-host-ip>:8123`.
- Complete the onboarding wizard. Confirm you can create an automation.

## Uninstall / Clean up
```bash
docker stop homeassistant && docker rm homeassistant
rm -rf ~/ha-config
```

## Troubleshooting
- **Port 8123 already in use**: Stop conflicting services or change the container port mapping.
- **Config errors**: Check the container logs:
```bash
docker logs -f homeassistant
```
