# ☸️ Kubernetes `kubectl` Commands Cheat Sheet

> **Note:** Use `kubectl --help` or `kubectl <command> --help` for full option details.  
> Switch namespace with `-n <namespace>`.

---

## 🔎 Cluster Info
```bash
kubectl version --short          # Client & server versions
kubectl cluster-info             # Cluster master & DNS info
kubectl config view --minify     # Show current context
kubectl get nodes                # List cluster nodes
kubectl describe node <node>     # Detailed node info
```

---

## 📦 Workloads

### Pods
```bash
kubectl get pods                 # Pods in current namespace
kubectl get pods -A              # Pods in all namespaces
kubectl describe pod <pod>       # Detailed info
kubectl logs <pod>               # Show pod logs
kubectl logs -f <pod>            # Stream logs
kubectl exec -it <pod> -- sh     # Shell into pod
kubectl delete pod <pod>         # Delete pod
```

### Deployments
```bash
kubectl get deployments          # List deployments
kubectl describe deployment <d>  # Details
kubectl scale deployment <d> --replicas=3   # Scale up/down
kubectl rollout status deployment <d>       # Check rollout
kubectl rollout undo deployment <d>         # Rollback
```

### ReplicaSets & StatefulSets
```bash
kubectl get rs                   # List ReplicaSets
kubectl get statefulsets         # List StatefulSets
```

---

## 🌐 Services & Networking
```bash
kubectl get svc                  # List services
kubectl describe svc <svc>       # Service details
kubectl expose deployment <d> --type=NodePort --port=8080
kubectl get ingress              # List ingresses
kubectl describe ingress <ing>   # Ingress details
```

---

## 📂 Config & Secrets
```bash
kubectl get configmaps
kubectl describe configmap <cm>
kubectl get secrets
kubectl describe secret <secret>
kubectl create secret generic mysecret --from-literal=key1=supersecret
```

---

## 🗂 Namespaces
```bash
kubectl get ns                   # List namespaces
kubectl create ns dev            # Create new namespace
kubectl delete ns dev            # Delete namespace
kubectl get pods -n kube-system  # Get pods in kube-system
```

---

## ⚡ Apply & Manage Resources
```bash
kubectl apply -f file.yaml       # Create/update from YAML
kubectl delete -f file.yaml      # Delete resources from YAML
kubectl get all                  # Get all resources in ns
kubectl explain pod.spec         # Show API schema
```

---

## 🛠 Troubleshooting
```bash
kubectl describe pod <pod>       # Events & reasons for failures
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl top pod                  # Resource usage (needs metrics-server)
kubectl top node                 # Node usage
kubectl get pods -o wide         # Show node assignment, IPs
```

---

## 🔑 Contexts & Config
```bash
kubectl config get-contexts      # List contexts
kubectl config use-context <ctx> # Switch context
kubectl config current-context   # Show active context
```

---

## 🧹 Useful Shortcuts
```bash
kubectl get po                   # Short for pods
kubectl get deploy               # Short for deployments
kubectl get svc                  # Short for services
kubectl get ns                   # Short for namespaces
```

---

## 🚀 Common Workflows

- **Debugging a pod**  
  ```bash
  kubectl exec -it <pod> -- sh
  kubectl logs -f <pod>
  kubectl describe pod <pod>
  ```

- **Rolling update**  
  ```bash
  kubectl set image deployment/<d> <container>=<image>:<tag>
  kubectl rollout status deployment/<d>
  ```

- **Dry run to YAML**  
  ```bash
  kubectl create deployment nginx --image=nginx --dry-run=client -o yaml
  ```

---
