# k8s-manifests

Plain Kubernetes YAML for the banking application (no Kustomize).

## Structure
- `dev/`      : everything applied to the dev namespace (numbered = apply order)
- `examples/` : fake secret, reference only, never applied

## Deploy to dev
```bash
kubectl apply -f dev/00-namespace.yaml
kubectl create secret generic auth-secrets -n dev \
  --from-literal=DB_PASSWORD='<password>' \
  --from-literal=JWT_SECRET="$(openssl rand -base64 32)"
kubectl apply -f dev/
kubectl get pods,pvc -n dev
```