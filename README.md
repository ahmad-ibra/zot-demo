# zot-demo
This is the repo for Zot demo showcased in [my video](https://youtu.be/zOjOF00aQSY)
## Create Kubernetes cluster
```
kind create cluster --config kind-config.yaml
```
## Install cert manager 
```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.12.0/cert-manager.yaml
```

## Install Nginx nginx controller 
```
kubectl apply -f nginx.yaml
```
## Create certificate issuer
```
kubectl apply -f clusterissuer.yaml
```

## Install Zot 

```
helm repo add project-zot http://zotregistry.io/helm-charts
helm repo update project-zot
helm install zot project-zot/zot -f values.yaml
```

## Push and Pull 

```
First install Skopeo (brew install skopeo)
skopeo --insecure-policy copy --dest-tls-verify=false --multi-arch=all \
   --format=oci docker://saiyam911/wsmblr --dest-creds admin:admin \
   docker://zot.<change to your nginx LB DNS>/saiyam:latest
```
