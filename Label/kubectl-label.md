# kubectl label

Allows you to change add edit and delete labels on resources.

``` shell
  k run test-pod --image nginx $dry > pod.yaml 
  kubectl create -f pod.yaml

  # Update all pods in the namespace
  kubectl label pods/test-pod status=ok 
  kubectl label pods -l status=ok app=run
  kubectl label pods -l status=unhealthy --overwrite
  kubectl label pods -l status=ok --overwrite --list
  kubectl label pods --all env=prod name=norway --list
  kubectl label pods test-pod env-


  # Update a pod identified by the type and name in "pod.yaml"
  kubectl label -f pod.yaml env=prod --list
  
  # you can find the resource version inside the metadata
  kubectl label pods foo status=unhealthy --resource-version=2615649


```
