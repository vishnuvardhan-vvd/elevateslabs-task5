
# Task : Build a Kubernetes Cluster Locally with Minikube

# Objective
Deploy and manage applications in a local Kubernetes environment using Minikube.

---

# Tools & Requirements
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Docker](https://www.docker.com/)

---

# Setup Instructions

 1. Install Dependencies
Make sure the following tools are installed on your local machine:
- Docker
- kubectl
- Minikube

To verify installation:
```bash
docker --version
kubectl version --client
minikube version
```

---

#2. Start Minikube Cluster
```bash
minikube start
```

To verify the cluster is running:
```bash
kubectl cluster-info
```

---

# Deploy an App

# 3. Create `deployment.yaml`

Create a Kubernetes Deployment configuration for your app. Example:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: nginx
        ports:
        - containerPort: 80
```

Apply the deployment:
```bash
kubectl apply -f deployment.yaml
```

---

# 4. Create `service.yaml`

Expose your app via a service:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

Apply the service:
```bash
kubectl apply -f service.yaml


# Verify and Manage

# 5. Check Running Pods
```bash
kubectl get pods
```

# 6. View Services
```bash
kubectl get services
```

# 7. Scale the Deployment
```bash
kubectl scale deployment my-app-deployment --replicas=4
```

# 8. Describe Resources
```bash
kubectl describe deployment my-app-deployment
kubectl describe pod <pod-name>
```

# 9. View Logs
```bash
kubectl logs <pod-name>
```

---

# Deliverables

- YAML Files:
  - `deployment.yaml`
  - `service.yaml`
- Screenshots:
  - Output of `kubectl get pods`
  - Output of `kubectl get services`
  - Output of `kubectl describe deployment`
  - Output showing scaling in action

---

# Summary

This task walks through the basics of creating and managing a Kubernetes application locally with Minikube. You should now be comfortable with:
- Starting a Minikube cluster
- Deploying an app via Kubernetes manifests
- Exposing your app to external traffic
- Scaling and inspecting Kubernetes workloads
