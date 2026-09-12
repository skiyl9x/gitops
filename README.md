# GitOps

Add Flux Operator
```
helm install flux-operator oci://ghcr.io/controlplaneio-fluxcd/charts/flux-operator \
  --namespace flux-system \
  --create-namespace
```

Install Flux into Production Cluster
```
git clone git@github.com:skiyl9x/gitops.git
kubectl apply -f gitops/clusters/production/flux-instance.yaml
```

```
ssh-keygen -t ed25519 -C "flux@github.com"

flux create secret git flux-system   --url=ssh://git@github.com/skiyl9x/gitops   --private-key-file=github-flux  --password="github-flux"   --namespace=flux-system
```
