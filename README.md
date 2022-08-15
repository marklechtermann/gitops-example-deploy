# GitOps 

## Install ArgoCD

```bash
kubectl apply -k installation/argocd
```

## Install sealed-secrets

```bash
kubectl apply -f installation/sealed-secrets/manifest.yaml
```

Install cli:   
```bash
mkdir kubeseal && \
curl -L -o kubeseal/kubeseal.tgz https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.18.1/kubeseal-0.18.1-linux-amd64.tar.gz && \
tar -C kubeseal -xzf kubeseal/kubeseal.tgz && \
sudo install kubeseal/kubeseal /usr/local/bin/ && \
rm -rf kubeseal
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
kubectl apply -f app-of-apps/manifest.yaml
```

## Create a new sealed-secret

```bash
echo -n 1234567 | kubectl create secret generic mysecret -n development --dry-run=client --from-file=foo=/dev/stdin -o yaml  | kubeseal > /home/markl/git/github/gitops-example-deploy/deployments/overlays/development/sealed-secret.yaml

echo -n abcdef | kubectl create secret generic mysecret -n production --dry-run=client --from-file=foo=/dev/stdin -o yaml  | kubeseal > /home/markl/git/github/gitops-example-deploy/deployments/overlays/production/sealed-secret.yaml

echo -n xyz | kubectl create secret generic mysecret -n staging --dry-run=client --from-file=foo=/dev/stdin -o yaml  | kubeseal > /home/markl/git/github/gitops-example-deploy/deployments/overlays/staging/sealed-secret.yaml
```
