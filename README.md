# Kubernetes

## First commands

```sh
kubectl create deployment nginx-sample --image=nginx --port=80 --replicas=3
kubectl get pods
kubectl expose deployments/nginx-sample --type="NodePort" --port 80
# kubectl expose rc nginx --port=80 --target-port=8000

kubectl delete service nginx-sample
kubectl delete deployment nginx-sample

kubectl get pods
```

## Main service

```
mkdir www
echo "<p>This is the main site</p>" > www/index.html
kubectl create configmap mysite-html --from-file www
kubectl apply -f 1-main.yaml
```

## Second service

Serving `/assets` on top of the previous service

```
mkdir assets
echo "<p>Here are the assets</p>" > assets/index.html
kubectl create configmap assets-html --from-file assets
kubectl apply -f 2-assets.yaml
```

## TLS

```sh
kubectl create namespace cert-namager
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.yaml
kubectl apply -f 3-letsencrypt-issuer-staging-yaml
```

## Cleanup

```sh
kubectl delete -f starter1-yaml
kubectl delete -f starter1-assets.yaml
kubectl delete configmap mysite-html
kubectl delete configmap assets-html
kubectl delete certificate myservice-certificate
kubectl delete clusterissuers letsencrypt-staging
```

## Cheatsheet

```sh
k get all
k get pods
k get deployments
k get services
k get configmaps
k get clusterissuers
k get secrets
k get certificates
k get certificaterequests
k get orders
k get challenges
```
