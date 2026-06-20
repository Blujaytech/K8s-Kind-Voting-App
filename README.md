# k8s-kind-voting-app

A sample cloud-native voting application designed to demonstrate Kubernetes orchestration using [kind](https://kind.sigs.k8s.io/). This project showcases a microservices-based architecture with .NET, Redis, PostgreSQL, and Kubernetes.
K8s Kind Voting App – Project Overview
Project Name: K8s Kind Voting Application with GitOps Deployment
GitHub Repository: K8s Kind Voting App Repository

# Project Overview

The K8s Kind Voting App is a cloud-native microservices application deployed on a Kubernetes cluster created using Kind (Kubernetes in Docker). The project demonstrates end-to-end Kubernetes deployment, GitOps automation using Argo CD, monitoring with Prometheus and Grafana, and container orchestration using Docker and Kubernetes. The application allows users to vote between two options and view real-time results through a distributed microservices architecture.

# TechStack
1. Aws EC2 - 2 Servers (EKS/ArgoCD/Docker).
2. Git,ArgoCD,Docker,Aws Eks.

## Architecture Overview


<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/97b29c09-7ea9-4a79-94e3-eef1ebdc1fa2" />



```
+----------------+      +----------------+      +------------------+
|                |      |                |      |                  |
|   Web Frontend +----->+   API Server   +----->+   PostgreSQL DB  |
|  (Voting App)  |      | (.NET Core)    |      |                  |
|                |      |                |      +------------------+
+----------------+      |                |
                        |                |      +------------------+
                        |                +----->+   Redis Cache    |
                        |                |      |                  |
                        +----------------+      +------------------+
                                |
                                v
                        +----------------+
                        |    Worker      |
                        | (.NET Worker)  |
                        +----------------+
```

- **Web Frontend**: User interface for voting and viewing results.
- **API Server**: Handles business logic, connects to Redis and PostgreSQL.
- **Redis**: Caching layer for fast vote tallying.
- **PostgreSQL**: Persistent storage for votes and results.
- **Worker**: Background service for processing votes from Redis to PostgreSQL.

---

## Features

- Vote for your favorite option in real-time.
- Results update live using Redis pub/sub.
- Scalable microservices, each in its own container.
- Easily deployable to a local Kubernetes cluster using kind.

---

## Prerequisites

- [Docker](https://www.docker.com/)
- [kind](https://kind.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [.NET 7 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)

---

## Getting Started

1. **Clone the repository:**
   ```sh
   git clone https://github.com/your-org/k8s-kind-voting-app.git
   cd k8s-kind-voting-app
   ```

2. **Build Docker images:**
   
   ```sh
   docker build -t voting-app-frontend ./frontend
   docker build -t voting-app-api ./api
   docker build -t voting-app-worker ./worker
   ```

3. **Create a kind cluster:**
   ```sh
   kind create cluster --name voting-app
   ```

4. **Deploy to Kubernetes:**
   ```sh
   kubectl apply -f k8s/
   ```

5. **Access the app:**
   - Find the service URL using `kubectl get svc`.

---

## Project Structure

```
k8s-kind-voting-app/
├── api/         # .NET Core API server
├── frontend/    # Web frontend (React/Angular/etc.)
├── worker/      # .NET Worker service
├── k8s/         # Kubernetes manifests
└── README.md
```

---

## Technologies Used

- .NET 7
- StackExchange.Redis
- Npgsql (PostgreSQL)
- Newtonsoft.Json
- Kubernetes (kind)
- Docker

---

## License

MIT License

### Project installation Process :

ArgoCD Deployment for K8s Kind Voting App

1. Create ArgoCD Namespace
   
```
kubectl create namespace argocd
```

Explanation: Creates a dedicated namespace for ArgoCD resources.

2. Verify Namespace Creation
   
```
kubectl get ns
```

Explanation: Lists all namespaces and confirms the argocd namespace exists.

3. Install ArgoCD
   
```
kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Explanation: Installs all ArgoCD components (Server, Controller, Repo Server, Redis, etc.) in the argocd namespace.

4. Clone Application Repository
   
```
git clone https://github.com/Blujaytech/K8s-Kind-Voting-App.git
```
Explanation: Downloads the Voting Application source code and Kubernetes manifests from GitHub.

5. Navigate to Project Directory
   
```
cd K8s-Kind-Voting-App/
```
Explanation: Moves into the project folder.

6. Verify Project Files
   
```
ls
```
Explanation: Lists project files and directories.

7. Verify ArgoCD Pods
   
```
kubectl get pods -A
```
Explanation: Displays pods running across all namespaces to ensure ArgoCD components are healthy.

8. Verify Docker Containers
   
```
docker ps
```
Explanation: Lists running Docker containers on the server.

9. Check ArgoCD Services
    
```
kubectl get svc -n argocd

```
Explanation: Displays ArgoCD services and their ports.

10. Expose ArgoCD Server
    
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

```
Explanation: Changes the ArgoCD server service type from ClusterIP to LoadBalancer for external access.

11. Verify LoadBalancer Service
    
```
kubectl get svc -n argocd

```
Explanation: Confirms the external endpoint assigned to the ArgoCD server.

12. Retrieve ArgoCD Admin Password
    
```
kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

```
Explanation: Retrieves the default admin password for ArgoCD login.

```
Username: admin

```
13. Verify Application Pods
    
```
kubectl get pods

```
Explanation: Displays application pods running in the current namespace.

14. Verify Application Services
    
```
kubectl get svc

```
Explanation: Lists application services and exposed ports.

15. Access Vote Application
    
```
kubectl port-forward svc/vote 5000:5000 --address=0.0.0.0 &

```
Explanation: Exposes the Vote application on port 5000.

Access URL:

```
http://<SERVER_PUBLIC_IP>:5000

```
16. Access Result Application
    
```
kubectl port-forward svc/result 5001:5001 --address=0.0.0.0 &
```
Explanation: Exposes the Result application on port 5001.


Access URL:

```
http://<SERVER_PUBLIC_IP>:5001

```

