------------------------------kubectl------------------------------
   ```
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   ```

   ```
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
   ```
   ```
   chmod +x kubectl
   ```
   ```
   mv kubectl /usr/local/bin/
   ```
   ```
   kubectl version --client
   ```
-------------------------eksctl------------------------------------
   ```
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   ```
   ```
   mv /tmp/eksctl /usr/local/bin
   ```
   ```
   eksctl version
   ```

   ```
   eksctl create cluster --name blujay-cluster --region us-east-1 --nodegroup-name demo-nodes --node-type t3.small --nodes 2
   ```
   
   ```
   eksctl delete cluster --name blujay-cluster --region us-east-1
   ```
   ```
   kubectl get nodes
   ```
----------------------k9s-Installation-----------------------------
```
curl -sS https://webinstall.dev/k9s | bash
```

```
export PATH=$PATH:$HOME/.local/bin
```

------------------------------------------------------------
