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

## 4. Create ArgoCD deployment
Create a config with links to your github.com repository (check how I did it here: argocd/applications/kuber.yaml)

## 5. Run application
Apply deployment to run your application in ArgoCD 
```sh
kubectl apply -f argocd/applications/kuber.yaml
```
<img width="1505" alt="Screenshot 2023-06-15 at 13 25 57" src="https://github.com/KsantaKislova/K8s/assets/55740985/c5ac5313-332f-42fb-91c3-14ef94d252d3">

