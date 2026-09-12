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
kubectl apply gitops/clusters/production/flux-instance.yaml
```
