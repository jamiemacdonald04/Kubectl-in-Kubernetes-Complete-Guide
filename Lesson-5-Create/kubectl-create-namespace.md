# kubectl create namespace

## namespace

Lets explore creating a namespace

``` shell
kubectl create namespace my-first-namespace --dry-run=client -o yaml
kubectl create namespace my-first-namespace
kubectl create deployment test-deploy --image nginx -n my-first-namespace
kubectl get pods -n my-first-namespace
kubectl get pods -n my-first-namespace
```
