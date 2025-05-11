# Lab 3: Using Minikube to Create a Cluster

**Objective:** Start a local Kubernetes cluster using Minikube and understand its components.

------- 

## **1. Introduction to Kubernetes Clusters**

### Key Concepts:

- **Control Plane**: Manages the cluster (scheduling, scaling, updates).
- **Nodes:** Worker machines that run applications (VMs or physical machines).
- **Minikube:** A tool to create a single-node Kubernetes cluster for local development.

Cluster Diagram:

![Cluster Diagram](./assets/module_01_cluster.svg)

---

## **2. Setting Up Minikube**

### Steps:

1. **Prerequisites:**

- Enable virtualization (VT-x/AMD-V) in BIOS.
- Install a hypervisor (e.g., Docker Desktop, VirtualBox, or HyperKit).

2. **Install Minikube:**
```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

**Verification:**
```bash
minikube version
```

Screenshot of successful installation:
![Minikube Version](./assets/minikubeInstall.png)
