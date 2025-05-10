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
