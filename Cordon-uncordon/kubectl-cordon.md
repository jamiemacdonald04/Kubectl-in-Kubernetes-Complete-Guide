# kubectl cordon
The `kubectl cordon` command is used to mark a node as unschedulable. 
This command is aimed at nodes and will not allow anything to be scheduled on a node that has been cordoned.
After cordoning the status will be "Ready,SchedulingDisabled"

``` shell
# test deployment 
kubectl create deployment front-end --replicas 2 --image redis

# note name and node status
kubectl get nodes 
# choose the name of a node and substitute where I have put minikube. (minikube is the default node name)
kubectl cordon minikube
kubecl get nodes 

kubectl create deployment back-end --replicas 2 --image redis
kubectl scale deployment front-end --replicas 0
kubectl scale deployment front-end --replicas 2

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
