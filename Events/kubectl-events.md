# Kubectl Events

The `kubectl events` is a command that is used to get the events that are happening in the cluster. 
This is useful when you are trying to debug an issue in the cluster.

## Events
Let's run the various commands and arguments that are available with the `kubectl events` command.

``` shell
kubectl create namespace food
kubectl run curry --image=nginx -n food -- false
kubectl events -n food
kubectl describe pod curry -n food

# by type 
kubectl events -n food --types=Warning

# watch for this gotcha 
kubectl events --for=pod/curry -n food --types=Warning
kubectl events pod curry -n food --types=Warning
kubectl run fishchips --image=nginx -n food -- false
kubectl events pod curry -n food --types=Warning
kubectl events --for=pod/fishchips -n food --types=Warning

# no header and output as yaml
kubectl events -n food --no-headers
kubectl events -n food --no-headers -o yaml

# all namespaces 
kubectl events -A

# with a watch 
kubectl events -n food --watch
kubectl run maccheese --image=nginx -n food 
```
