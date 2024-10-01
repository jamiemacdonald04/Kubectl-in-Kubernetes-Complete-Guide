# kubectl top

Retrieve the memory and cpu usage for the pod or node.  

``` shell
kubectl create namespace trades
kubectl create deploy plumber --image=nginx --replicas=2 -n trades
kubectl create deploy brick-layer --image=nginx --replicas=2 -n trades
kubectl top pods -n trades
kubectl top nodes -n trades
```

## error: Metrics API not available

Metrics are perhaps not enabled. To enable in minikube run the following command

``` shell
# only use first statement if using minikube to set up metrics-server.
minikube addons enable metrics-server
```

## error: metrics not available yet

Perhaps pods are not started yet. Give it a bit of time and try again.

## error: Metrics not available for pod default/test-match-67754546-69htz, age: 3m45.395759s

Check that there are no errors in the deployment or with the running pod above and restart minikube.  There is also a known issue with some versions of minikube try restarting with the following commands.

``` shell
minikube stop
minikube start --extra-config=kubelet.housekeeping-interval=10s 
```

# alternatively you can use the following command to get the metrics

``` shell
# set up metrics 
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl -n kube-system edit deployments.apps metrics-server
#edit with yaml below
```

```yaml
command:
- /metrics-server
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP

```
