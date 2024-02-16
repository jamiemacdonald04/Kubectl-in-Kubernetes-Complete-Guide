# kubectl scale

If the object has replicas you can use it to scale  up and down the replicas and in some cases to manafest edits you have made to the object.  For example statefulsets and deployments can all be scaled or you can scale the replicaSet associated with these.

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
