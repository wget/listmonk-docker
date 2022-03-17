# listmonk-docker

This repo has been provided in order to offer a minimum working example of listmonk with a working config that can be deployed within minutes.

Indeed, the default Docker compose file provided by listmonk is too complex to deploy/configure properly for a simple demo.

## Testing recipe

These instructions take Debian as example.

### Install Docker

```
apt remove -y docker docker-engine docker.io containerd runc
apt update
apt dist-upgrade -y
apt install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

apt update
apt install docker-ce docker-ce-cli containerd.io -y
```

### Install the new Docker Compose version

Install the Docker Compose V2 still proposed as an extension from now ([src.](https://docs.docker.com/compose/cli-command/#install-on-linux)):
```
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
docker compose version
```

### Deploy listmonk

To test, just clone this repo:

```
git clone https://github.com/wget/listmonk-docker.git
cd listmonk-docker
docker compose -f docker-compose.yml up -d
```

Visit http://localhost:9000 and you should fall on the admin interface of listmonk.

The default credentials are `listmonk` both for the username and password.
