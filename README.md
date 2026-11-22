# k8s-manifests

Kubernetes manifests for the banking application (Kustomize).

## Structure
- `base/`     : shared by every environment (postgres, auth-service, config, ingress)
- `overlays/` : per-environment values (namespace, image tag, replicas)
- `base/postgres/secret.example.yaml` : fake values, reference only, never applied

## Deploy to dev
```bash
kubectl apply -f overlays/dev/namespace.yaml
kubectl create secret generic auth-secrets -n dev \
  --from-literal=DB_PASSWORD='<password>' \
  --from-literal=JWT_SECRET="$(openssl rand -base64 32)"
kubectl apply -k overlays/dev
kubectl get pods,pvc -n dev
```

Preview without applying: `kubectl kustomize overlays/dev`