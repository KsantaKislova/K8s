# K8s & ArgoCD

In this topic I want to show how to deploy containerized application with ArgoCD (GitOps approach) .

## 1. Up ArgoCD
Install ArgoCD with kubectl (documentation: https://argo-cd.readthedocs.io/en/stable/getting_started/)
```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Install ArgoCD-cli tool
```sh
brew install argocd
```
Do port-forwarding to make your ArgoCD UI available from your local machine (localhost:8080)
```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Extract password to login with username: admin
```sh
argocd admin initial-password -n argocd
```

## 2. Create project
Create project with k8s config (for me it's "development" or "infrastructure"), check in my project here: argocd/projects/dev.yaml
Deploy it: 
```sh
kubectl apply -f argocd/projects/dev.yaml
```

## 3. Create k8s resources you want to add
You can check them also by following this path: dev/kuber/deployment.yaml and dev/kuber/svc.yaml

## 4. 
