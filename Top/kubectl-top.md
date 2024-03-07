# kubectl top

Retrieve the memory and cpu usage for the pod or node.  

``` shell
kubectl top pods 
kubectl top nodes
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
