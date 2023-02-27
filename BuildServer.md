# Initial Configure

> Update / Upgrade

```Bash
sudo apt update --upgrade
```

> Root Password

```Bash
sudo passwd root
# M4rcos@123
```

> Add Swap Space

```Bash
fallocate -l 4G /swapfile 
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo /swapfile swap swap defaults 0 0 >> /etc/fstab
swapon --show
free -h
sysctl vm.swappiness=10
```

> Remove Swap Space

```Bash
swapoff -v /swapfile
rm /swapfile
```

> Instal Docker

```Bash
apt install ca-certificates curl gnupg lsb-release
mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# Verify that the Docker Engine installation is successful
docker run hello-world
```

> Unistall Docker

```Bash
apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
rm -rf /var/lib/docker
rm -rf /var/lib/containerd
```

> Install Portainer

```Bash
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:latest
docker ps
# https://localhost:9443
```