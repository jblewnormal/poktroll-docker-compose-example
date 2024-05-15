# tl;dr Hetzner Ubuntu Setup <!-- omit in toc -->

:::warning Olshansky's docs

This is a tl;dr copy-pasta (by & for Olshansky) while setting up a Hetzner server.
It is not intended to act as proper documentation so use at your own risk.

:::

- [General](#general)
- [Dependencies](#dependencies)
  - [Install Docker](#install-docker)
  - [Install docker-compose](#install-docker-compose)
  - [bashrc](#bashrc)
- [Pocket Logic](#pocket-logic)

## General

- Set up your server on [hetzner's console](https://console.hetzner.cloud/projects/)
- Avoid using arm architecture since we do not build images for it yet
- Ssh into your server with: `ssh root@...`

## Dependencies

### Install Docker

Ref [here](https://docs.docker.com/engine/install/ubuntu/)

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
 "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
 $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
 sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Install docker-compose

Ref [here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### bashrc

````bash

## Pocket Setup

```bash

docker rm $(docker ps -aq) -f

git clone https://github.com/pokt-network/poktroll-docker-compose-example.git
cd poktroll-docker-compose-example

curl https://raw.githubusercontent.com/pokt-network/pocket-network-genesis/master/poktrolld/testnet-validated.json > poktrolld-data/config/genesis.json

cp .env.sample .env
sed -i -e s/YOUR_NODE_IP_OR_HOST/.../g .env
````

## Pocket Logic

```bash
source helpers.sh

poktrolld keys add relayminer-1
export SUPPLIER_ADDR=pokt15l3gamxkz5c5pz9ynk0xqmkq6m07k5jcn89cl9

```
