# GitOps

The architecture is adapted from this fluxcd repository - [flux2-kustomize-heml-example](https://github.com/fluxcd/flux2-kustomize-helm-example)


Command to delete all resources: 

```
flux uninstall --namespace=flux-system
```

Command to bootstrap everything from scratch

```
flux bootstrap git --url=ssh://git@github.com/skiyl9x/portfolio --branch=main --private-key-file=../github-fluxcd-portfolio --password=fluxcd --path=clusters/dev --namespace=flux-system
```

Enable storage-provisioner-rancher for minikube
```
minikube addons enable storage-provisioner-rancher
```



Enable LoadBalancer(metallb) for minikube
```
minikube addons enable metallb
```

```
oshyd@1H851821G3:~/MyProjects/portfolio/infrastructure/base/configs/metallb$ minikube ip
192.168.39.162
oshyd@1H851821G3:~/MyProjects/portfolio/infrastructure/base/configs/metallb$ minikube addons configure metallb
-- Enter Load Balancer Start IP: 192.168.39.180
-- Enter Load Balancer End IP: 192.168.39.200
    ▪ Using image quay.io/metallb/speaker:v0.9.6
    ▪ Using image quay.io/metallb/controller:v0.9.6
✅  metallb was successfully configured
```

Add next to the /etc/hosts
```
192.168.39.180  traefik-dashboard.dev.skiyl9x.pp.ua whoami.dev-01.skiyl9x.pp.ua nginx.dev-01.skiyl9x.pp.ua rabbitmq.dev.skiyl9x.pp.ua flux-web.dev.skiyl9x.pp.ua grafana.dev.skiyl9x.pp.ua whoami.stage-01.skiyl9x.pp.ua nginx.stage-01.skiyl9x.pp.ua whoami.prod-01.skiyl9x.pp.ua  nginx.prod-01.skiyl9x.pp.ua dev-01.skiyl9x.pp.ua stage-01.skiyl9x.pp.ua prod-01.skiyl9x.pp.ua

```


Create secret to get access to the Docker Registry

```
kubectl create secret docker-registry github-oci-auth --namespace=flux-system --docker-server=ghcr.io --docker-username=skiyl9x --docker-password=<github-token>
```


Create secret for CloudFlare API (required for automatic SSL generation)
```
kubectl create secret generic cloudflare-api-token \
  --from-literal=api-token=YOUR_TOKEN_HERE -n cert-manager-system
```
