# kubectl scale

The `kubectl scale` command is used to scale the number of replicas in a deployment, replicaSet, or statefulSet.
For example statefulsets and deployments can all be scaled or you can scale the replicaSet associated with these.
This can also be done to elevate issues such as split brain, by scaling to 0 and then back up to the desired number of replicas.

``` shell

Lets go ahead and create a deployment and scale it from 1 to 3.

``` shell
kubectl create deployment database --replicas=2 --image nginx
kubectl create deployment front-end --replicas=2 --image nginx

kubectl scale deployment/front-end --replicas=3 
```

Now lets say you want to scale based on label.

``` shell

kubectl label deployment database front-end prod=live
kubectl scale deployment -l prod=live --replicas=0 

```

Now lets do a neat trick to bring them back up based on their currrent count of replicas.  We will create a deployment called redis with 4 replicas so that we can see that this is not touched as it does not meet the requirement.

```shell
kubectl create deployment redis --replicas=4 --image nginx
kubectl scale deployment --current-replicas=0 --replicas=3 --all
```
