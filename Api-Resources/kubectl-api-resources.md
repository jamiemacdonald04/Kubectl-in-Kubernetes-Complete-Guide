# kubectl api-resources

## api-resources

The `kubectl api-resources` command  allows you to reference resources that you can use.  
We talk about how this will come in handy not just for the CKAD exam but also for day to day usage.

``` shell
k api-resources

kubectl api-resources --sort-by=name
kubectl api-resources --sort-by=kind

kubectl api-resources --namespaced=true
kubectl api-resources --namespaced=false

kubectl api-resources --no-headers

kubectl api-resources --api-group=storage.k8s.io

kubectl api-resources --verbs create
kubectl api-resources -o wide | grep -i pod 
```
