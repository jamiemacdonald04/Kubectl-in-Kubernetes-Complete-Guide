# kubectl annotate

## api versions

Allows you to change add edit adn delete anotations on resources.  Lets explore this in more detail.

``` shell
  k run test-pod $dry > pod.yaml 
  kubectl create -f pod.yaml

  # Update all pods in the namespace
  kubectl annotate pods/test-pod -l status=ok app=run
  kubectl annotate pods -l status=ok app=run
  kubectl annotate pods -l status=unhealthy --overwrite
  kubectl annotate pods -l status=ok --overwrite --list
  kubectl annotate pods --all env=prod name=norway --list
  kubectl annotate pods test-pod env-


  # Update a pod identified by the type and name in "pod.json"
  kubectl annotate -f pod.yaml env=prod --list
  
  # you can find the resource version inside the metadata
  kubectl annotate pods foo status=unhealthy --resource-version=2615649


```
