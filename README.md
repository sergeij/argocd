## Prerequisites

### Install minikube (https://minikube.sigs.k8s.io/docs/start/)

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-arm64
sudo install minikube-darwin-arm64 /usr/local/bin/minikube
```

### Install Docker Desktop (https://docs.docker.com/desktop/install/mac-install/)

### Start minikube clusters

```bash
minikube start
minikube start -p minikube2 --apiserver-ips=192.168.1.223
```

### Install Argo

### Add clusters to Argo

```bash
argocd cluster add --label env=staging --insecure minikube --name staging-cluster --upsert
argocd cluster add --label env=production --insecure minikube2 --name production-cluster --upsert 
```

### Bootstrap cluster dependencies and applicationset

```bash
argocd login argocd.sco.ro
argocd repo add https://github.com/sergeij/argocd.git
argocd app create cluster-dependencies --repo https://github.com/sergeij/argocd.git --path bootstrap --dest-namespace sergeij --dest-server https://kubernetes.default.svc
```
