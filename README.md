# GitOps 

## Install ArgoCD

```bash
kubectl apply -k installation
```

Password:  

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```