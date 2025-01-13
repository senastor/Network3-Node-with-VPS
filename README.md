# Network3-Node-with-VPS

# Network3 Node Setup Tutorial

This tutorial provides step-by-step instructions to set up a Network3 node.

## Prerequisites
- A VPS with root access
- Docker and Docker Compose installed

## Steps

1. **Install Docker**:
   ```bash
   wget https://get.docker.com/ -O docker.sh
   sudo sh docker.sh

2. **Create a Directory for Configuration**
Create a directory for Network3 and navigate into it:
```bash
mkdir network3
cd network3
```

3. **Create the docker-compose.yml File**
Generate a new docker-compose.yml file:
```bash
touch docker-compose.yml
```
Edit the file with a text editor:

```bash
nano docker-compose.yml
```

**Paste the following content:**

```
version: '3.3'

services:
  network3-01:
    image: aron666/network3-ai
    container_name: network3-01
    environment:
      - EMAIL=your-email-to-bind
    ports:
      - 8080:8080/tcp
    volumes:
      - /path/to/wireguard:/usr/local/etc/wireguard
    healthcheck:
      test: curl -fs http://localhost:8080/ || exit 1
      interval: 30s
      timeout: 5s
      retries: 5
      start_period: 30s
    privileged: true
    devices:
      - /dev/net/tun
    cap_add:
      - NET_ADMIN
    restart: always
```
    
Configuration Details:
Replace your-email-to-bind with your Network3 email address.
Replace /path/to/wireguard with the actual path on your server.

4. **Start the Node**
Run the following command to start the Network3 node:
```bash
docker compose up -d
```

5. Verify the Setup
Check the status of your container:
```bash
docker compose ps
```


Troubleshooting
Port Conflict:
If you encounter an error like bind: address already in use, change the port in docker-compose.yml to an unused port.
Example:
```
ports:
  - 9091:8080/tcp
```
