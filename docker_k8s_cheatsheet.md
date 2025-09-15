# 🐳 Docker, Containers & Kubernetes — Cheat Sheet

> **Legal / ethical note:** Use these tools responsibly. Don’t interact with clusters, containers, or registries you don’t own or administer.

---

## Docker Basics

### Install & Verify
```bash
curl -fsSL https://get.docker.com | sh
docker --version
docker run hello-world
```

### Core Commands
- **Images**
  ```bash
  docker pull <image>
  docker images
  docker rmi <image>
  ```
- **Containers**
  ```bash
  docker run -it <image> /bin/bash
  docker ps -a
  docker stop <id> && docker start <id>
  docker rm <id>
  ```
- **Build**
  ```bash
  docker build -t <tag> .
  ```
- **Logs & Exec**
  ```bash
  docker logs <id>
  docker exec -it <id> sh
  ```
- **Networks & Volumes**
  ```bash
  docker network ls
  docker network inspect <network>
  docker volume ls
  docker volume inspect <volume>
  ```

---

## Containers (OCI Concepts)
- **Image** → immutable filesystem + metadata  
- **Container** → running instance of an image  
- **Registry** → where images are stored (Docker Hub, GCR, ECR)  
- **Orchestration** → managing many containers (Kubernetes, Docker Swarm)  

---

## Kubernetes Basics

### Install & Contexts
```bash
minikube start
kind create cluster
kubectl config get-contexts
kubectl config use-context <name>
```

### Core Commands
- **Cluster Info**
  ```bash
  kubectl cluster-info
  kubectl get nodes
  kubectl describe node <name>
  ```
- **Workloads**
  ```bash
  kubectl get pods
  kubectl describe pod <name>
  kubectl logs <pod>
  kubectl exec -it <pod> -- sh
  ```
- **Deployment & Services**
  ```bash
  kubectl apply -f <file>.yaml
  kubectl delete -f <file>.yaml
  kubectl get deployments
  kubectl expose deployment <name> --type=NodePort --port=8080
  ```
- **Namespaces**
  ```bash
  kubectl get ns
  kubectl -n <namespace> get pods
  ```

---

## Security & Best Practices

### Docker
- Use minimal base images (Alpine, distroless).  
- Don’t run as root inside containers.  
- Scan images (`docker scan <image>` or `trivy`).  
- Use secrets management (don’t hardcode env vars).  

### Kubernetes
- Use RBAC: restrict user/service account permissions.  
- Apply network policies: limit pod-to-pod comms.  
- Pod security: Pod Security Admission instead of PSPs.  
- Patch kubelet & API server regularly.  
- Monitor with Falco, kube-bench, kube-hunter.  

---

## Troubleshooting Quickies

### Docker
- “Cannot connect to the Docker daemon”  
  ```bash
  systemctl status docker
  ```
- Networking issues  
  ```bash
  docker network inspect bridge
  ```

### Kubernetes
- Pod stuck `CrashLoopBackOff`  
  ```bash
  kubectl logs <pod>
  ```
- Pod pending (resource issues)  
  ```bash
  kubectl describe pod <pod>
  ```
- DNS issues  
  ```bash
  kubectl -n kube-system get pods | grep dns
  ```

---

## Tools & Helpers
- **Docker Compose**: `docker-compose up -d`  
- **Lens**: GUI for Kubernetes  
- **Helm**: `helm install <chart>` for app packaging  
- **K9s**: terminal UI for Kubernetes  

---

## Quick Workflow Recap
1. **Build & test locally** with Docker.  
2. **Push image** to registry (Docker Hub, ECR, GCR).  
3. **Deploy** with `kubectl apply -f` or Helm.  
4. **Monitor logs**, resources, and scaling.  
5. **Secure** via RBAC, secrets, and image scanning.  
