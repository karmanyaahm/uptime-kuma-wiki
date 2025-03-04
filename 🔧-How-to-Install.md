- [🚀 Installer](#-installer-via-cli)
- [🐳 Docker](#-docker)
- [💪🏻 Without Docker](#-without-docker-recommended-for-x86x64-only)

## 🚀 Installer via CLI

[Ubuntu/CentOS] Interactive CLI installer, supports Docker or without Docker. 

```bash
curl -o kuma_install.sh http://git.kuma.pet/install.sh && sudo bash kuma_install.sh
```

## Advanced Installation

### 🐳 Docker

```bash
# Create a volume
docker volume create uptime-kuma

# Start the container
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

Browse to http://localhost:3001 after started.

Change Port and Volume

```bash
docker run -d --restart=always -p <YOUR_PORT>:3001 -v <YOUR_DIR OR VOLUME>:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

⚠️ Please use a **local volume** only. Other types such as NFS are not supported.

#### Docker Tags Description
<table>
    <thead>
      <tr>
<td>Tag(s)</td>
<td>Description </td>
</tr>
</thead>
<tbody>
<tr><td>latest, 1, 1.*</td><td>latest stable - debian</td></tr>
<tr><td>debian, 1-debian, 1.*-debian</td><td>latest stable - debian</td></tr>
<tr><td>❌alpine, 1-alpine, 1.*-alpine</td><td>(❌Deprecated due to DNS issues) latest stable - alpine</td></tr>
<tr><td>nightly*</td><td>development build, unstable</td></tr>
</tbody>
</table>

### 💪🏻 Without Docker (Recommended for x86/x64 only)

Required Tools: Node.js >= 14, git and pm2.

(**Not recommended for ARM CPU users.** Since there is no prebuilt for node-sqlite3, it is hard to get it running)

```bash
# Update your npm to the latest version
npm install npm -g

git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
npm run setup

# Option 1. Try it
node server/server.js

# (Recommended)
# Option 2. Run in background using PM2
# Install PM2 if you don't have: npm install pm2 -g
pm2 start server/server.js --name uptime-kuma

```

Browse to http://localhost:3001 after started.

```
# Listen to different port or hostname
pm2 start server/server.js --name uptime-kuma -- --port=80 --host=0.0.0.0
```

#### Useful Commands

```bash
pm2 start uptime-kuma
pm2 stop uptime-kuma
pm2 restart uptime-kuma

# Run at startup
pm2 startup
```

### Docker Compose Example

https://github.com/louislam/uptime-kuma/blob/master/docker/docker-compose.yml

## (Optional) One more step for Reverse Proxy

This is optional for someone who want to do reverse proxy.

Unlikely other web apps, Uptime Kuma is based on WebSocket. You need two more headers **"Upgrade"** and **"Connection"** in order to reverse proxy WebSocket.

Please read wiki for more info:
https://github.com/louislam/uptime-kuma/wiki/Reverse-Proxy


## Videos

- [Learn Uptime Kuma in 5 Minutes](https://www.youtube.com/watch?v=muZiPdH2JZ8) by DEVOPS UNLOCKED
  Install with the docker run command
- [Meet Uptime Kuma, a Fancy Open Source Uptime Monitor](https://www.youtube.com/watch?v=r_A5NKkAqZM) by Techno Tim
  Install with docker-compose
- [Monitor Status with Uptime Kuma - Let's install Uptime Kuma with Docker](https://www.youtube.com/watch?v=rRKvDMGeeBA) by Geeked
  Install with Portainer


## Unofficial & Experiment

⚠ ⚠ ⚠ Warning: Generally, I only test Docker and Node.js. All installation methods here may be broken in the future release. I don't maintain them. Use at your own risk.


### ☸️ Kubernetes (Unofficial)

⚠ Warning: K8s deployment is provided by contributors. I have no experience with K8s and I can't fix error in the future.

See more [here](https://github.com/louislam/uptime-kuma/tree/k8s-unofficial/kubernetes) 

### Ansible (Unofficial)

https://github.com/louislam/uptime-kuma/tree/ansible-unofficial/ansible

### Install on Synology NAS (Unofficial)

Unofficial tutorial by Marius Bogdan Lixandru:

https://mariushosting.com/how-to-install-uptime-kuma-on-your-synology-nas/

### Termux (Unofficial/Experiment)

Do you have an old Android phone? You could install Uptime Kuma on it!

https://github.com/louislam/uptime-kuma/issues/423

### Install on Azure Container Instance with TLS endpoint

Unofficial tutorial by Stefan:
https://haci.io/posts/uptime-kuma-azure-container-instance/