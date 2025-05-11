# Lab 2: Running Containers  
**Name:** Daniel Vetrila  
**Date:** 10 May 2025  

---

## **1. Setting Up Docker on Arch Linux**  

### **Installation**  
1. Install Docker and Docker Compose:  
   ```bash
   sudo pacman -S docker docker-compose

2. Start and enable the Docker service:  
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   
3. Add your user to the docker group (avoid sudo for Docker commands):  
   ```bash
   sudo usermod -aG docker $USER 
   newgrp docker # Refresh group membership


### Verification  
  ```bash
  docker --version
  docker run hello-world 
  ```

**Screenshot 1**: Hello World Verification
![Hello World](./assets/Screenshots/helloWorld)

---

## 2. Running Containers

### Publishing Ports

**Command:**  
```bash
docker run -d -p 8080:80 --name webserver nginx
```
- Access via http://localhost:8080.

**Screenshot 2**: Nginx Welcome Page
![Nginx](./assets/Screenshots/nginx)

### Overriding Container Defaults

**Command:**  
```bash
docker run -d -e POSTGRES_PASSWORD=secret -p 5432:5432 postgres
docker run -d -e POSTGRES_PASSWORD=secret -p 5433:5432 postgres
```

**Screenshot 3**: 2 Postgres Containers mapped to different ports running at the same time
![Postgres](./assets/Screenshots/postgres)

1. Create a compose.yml file with the following content:

```yaml
services:
  postgres:
    image: postgres
    entrypoint: ["docker-entrypoint.sh", "postgres"]
    command: ["-h", "localhost", "-p", "5432"]
    environment:
      POSTGRES_PASSWORD: secret 
```

2. Bring up the service by running the following command:
```bash
 docker compose up -d
``` 

3. Verify the authentication with Docker Desktop Dashboard.
```bash
 psql -U postgres
```

**Screenshot 4:** Override the default CMD and ENTRYPOINT in Docker Compose
![Docker Compose](./assets/Screenshots/postgresLogin)
