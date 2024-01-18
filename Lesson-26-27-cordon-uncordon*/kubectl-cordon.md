# kubectl cordon

This command is aimed at nodes and will not allow anything to be sheduled on a node that has been cordoned.
After cordoning the status will be "Ready,SchedulingDisabled"

``` shell
# note name and node status
kubectl get nodes 
# choose the name of a node and substitute where I have put minikube. (minikube is the default node name)
kubectl cordon minkube
kubecl get nodes 

# lets reset by using uncordon
kubectl uncordon minikube

# lets cordon again using label only 
kubectl label node minikube legacy=true
kubctl cordon -l legacy=true

# lets reset by using uncordon
kubectl uncordon minikube -l legacy=true

# all nodes should now have the status of ready again
kubectl get nodes 
```
