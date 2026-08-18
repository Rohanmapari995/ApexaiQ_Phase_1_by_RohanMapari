# Kubernetes Basic Commands

A beginner-friendly cheat sheet for commonly used Kubernetes (`kubectl`) commands.

## 1. What is kubectl?

`kubectl` is the command-line tool used to communicate with a Kubernetes cluster.

### General Syntax

```bash
kubectl <command> <resource> <name>
```

Example:

```bash
kubectl get pods
```

---

## 2. Cluster Information

### Check Kubernetes Version

```bash
kubectl version
```

### Get Cluster Information

```bash
kubectl cluster-info
```

### List All Nodes

```bash
kubectl get nodes
```

### Get Detailed Node Information

```bash
kubectl describe node <node-name>
```

---

## 3. Pods

A **Pod** is the smallest deployable unit in Kubernetes.

### List Pods

```bash
kubectl get pods
```

### List Pods with Additional Information

```bash
kubectl get pods -o wide
```

### Get Detailed Pod Information

```bash
kubectl describe pod <pod-name>
```

### View Pod Logs

```bash
kubectl logs <pod-name>
```

### Continuously View Logs

```bash
kubectl logs -f <pod-name>
```

### Enter a Running Container

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

### Delete a Pod

```bash
kubectl delete pod <pod-name>
```

---

## 4. Deployments

A **Deployment** manages the desired number of Pods.

### List Deployments

```bash
kubectl get deployments
```

### Create a Deployment

```bash
kubectl create deployment nginx --image=nginx
```

### Get Deployment Details

```bash
kubectl describe deployment <deployment-name>
```

### Scale a Deployment

```bash
kubectl scale deployment <deployment-name> --replicas=3
```

### Delete a Deployment

```bash
kubectl delete deployment <deployment-name>
```

---

## 5. Services

A **Service** provides network access to Pods.

### List Services

```bash
kubectl get services
```

### Create a Service

```bash
kubectl expose deployment nginx --port=80
```

### Get Service Details

```bash
kubectl describe service <service-name>
```

### Delete a Service

```bash
kubectl delete service <service-name>
```

---

## 6. YAML Files

Kubernetes resources are commonly defined using YAML files.

### Apply a YAML File

```bash
kubectl apply -f deployment.yaml
```

Creates or updates resources.

### Delete Resources from a YAML File

```bash
kubectl delete -f deployment.yaml
```

### Get Resources from a YAML File

```bash
kubectl get -f deployment.yaml
```

---

## 7. Namespaces

Namespaces are used to logically separate Kubernetes resources.

### List Namespaces

```bash
kubectl get namespaces
```

### Create a Namespace

```bash
kubectl create namespace mynamespace
```

### Get Pods from a Specific Namespace

```bash
kubectl get pods -n mynamespace
```

### Delete a Namespace

```bash
kubectl delete namespace mynamespace
```

---

## 8. Kubernetes Context

A context determines which Kubernetes cluster and configuration `kubectl` is using.

### List Contexts

```bash
kubectl config get-contexts
```

### Show Current Context

```bash
kubectl config current-context
```

### Switch Context

```bash
kubectl config use-context <context-name>
```

---

## 9. Get Kubernetes Resources

General syntax:

```bash
kubectl get <resource>
```

Examples:

```bash
kubectl get pods
kubectl get nodes
kubectl get deployments
kubectl get services
kubectl get replicasets
kubectl get namespaces
kubectl get configmaps
kubectl get secrets
```

### Get Common Resources

```bash
kubectl get all
```

---

## 10. Debugging Commands

### Describe a Pod

```bash
kubectl describe pod <pod-name>
```

### View Logs

```bash
kubectl logs <pod-name>
```

### View Live Logs

```bash
kubectl logs -f <pod-name>
```

### View Cluster Events

```bash
kubectl get events
```

### Check Node Resource Usage

```bash
kubectl top nodes
```

### Check Pod Resource Usage

```bash
kubectl top pods
```

---

## 11. Labels

### Show Pod Labels

```bash
kubectl get pods --show-labels
```

### Get Pods Using a Label

```bash
kubectl get pods -l app=nginx
```

---

# ⭐ Most Important Commands

| Command | Purpose |
|---|---|
| `kubectl get pods` | List Pods |
| `kubectl get nodes` | List Nodes |
| `kubectl get deployments` | List Deployments |
| `kubectl get services` | List Services |
| `kubectl describe pod <name>` | Show Pod details |
| `kubectl logs <pod>` | View Pod logs |
| `kubectl exec -it <pod> -- /bin/bash` | Enter a container |
| `kubectl apply -f file.yaml` | Create/update resources |
| `kubectl delete -f file.yaml` | Delete resources |
| `kubectl scale deployment <name> --replicas=3` | Scale Deployment |
| `kubectl get all` | Show common resources |
| `kubectl get events` | Show cluster events |
| `kubectl config current-context` | Show current context |
| `kubectl cluster-info` | Show cluster information |

---

# Basic Kubernetes Workflow

```bash
# 1. Check cluster
kubectl cluster-info

# 2. Check nodes
kubectl get nodes

# 3. Create a deployment
kubectl create deployment nginx --image=nginx

# 4. Check deployment
kubectl get deployments

# 5. Check pods
kubectl get pods

# 6. Create a service
kubectl expose deployment nginx --port=80

# 7. Check services
kubectl get services

# 8. Check pod logs
kubectl logs <pod-name>

# 9. Scale deployment
kubectl scale deployment nginx --replicas=3

# 10. Delete deployment
kubectl delete deployment nginx
```

---

# Kubernetes Command Flow

```text
                 Kubernetes Cluster
                        |
                     kubectl
                        |
        +---------------+---------------+
        |               |               |
      Create           Get            Delete
        |               |               |
   kubectl apply    kubectl get    kubectl delete
        |
        v
    Resources
        |
   +----+----+---------+
   |         |         |
  Pods   Deployments Services
```

---

# Quick Cheat Sheet

```bash
# Cluster
kubectl version
kubectl cluster-info
kubectl get nodes

# Pods
kubectl get pods
kubectl get pods -o wide
kubectl describe pod <pod>
kubectl logs <pod>
kubectl exec -it <pod> -- /bin/bash
kubectl delete pod <pod>

# Deployments
kubectl get deployments
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=3
kubectl delete deployment nginx

# Services
kubectl get services
kubectl expose deployment nginx --port=80
kubectl delete service <service>

# YAML
kubectl apply -f file.yaml
kubectl delete -f file.yaml

# Namespaces
kubectl get namespaces
kubectl create namespace mynamespace
kubectl get pods -n mynamespace

# Debugging
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get events
kubectl top nodes
kubectl top pods

# Context
kubectl config get-contexts
kubectl config current-context
kubectl config use-context <context>
```

---

# Learning Order

For beginners, learn Kubernetes in this order:

```text
1. kubectl
   ↓
2. Cluster & Nodes
   ↓
3. Pods
   ↓
4. Deployments
   ↓
5. Services
   ↓
6. YAML Files
   ↓
7. Namespaces
   ↓
8. ConfigMaps & Secrets
   ↓
9. Volumes
   ↓
10. Ingress
   ↓
11. StatefulSets
   ↓
12. RBAC
   ↓
13. Helm
```

---

## License

This cheat sheet is intended for learning and educational purposes.
