# GitOps 

## Install ArgoCD

```bash
kubectl apply -k installation
```

## Login into ArgoCD

http://argocd.127.0.0.1.nip.io

You can now log in to the ArgoCD UI. The default user is `admin`.  
To retrieve the password you can use the folden command:  

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

## App of Apps

Now all argocd apps can be installed:  

```bash
kubectl apply -f app-of-app/manifest.yaml
```