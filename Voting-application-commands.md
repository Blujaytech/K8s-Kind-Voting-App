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
