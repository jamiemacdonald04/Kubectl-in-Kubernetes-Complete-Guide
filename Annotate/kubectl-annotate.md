# kubectl annotate

## api versions

Allows you to change add edit adn delete anotations on resources.  Lets explore this in more detail.
pod
``` shell
  
  # First annotation
  kubectl run test-pod --image nginx
  kubectl run live-pod --image nginx
  kubectl annotate pod test-pod describe="this pod shows us what the power of annotations are"
  kubectl describe pod test-pod
  kubectl describe pod test-pod | grep -A3 Annotations 
  
  
  # Update all pods in the namespace
  kubectl label pod test-pod status=ok
  kubectl label pod live-pod status=ok
  # add an annotation 
  kubectl annotate pods -l status=ok app="is running full version"
  # repeat with different text will fail
  kubectl annotate pods -l status=ok app="is running half version"
  kubectl annotate pods -l status=ok app="is running full version" --overwrite
  
  #list out the annotations in a pod
  kubectl annotate pods -l status=ok --list
  # this does not annotate the pod
  kubectl annotate pods --all env=prod name=norway --list
  # this does 
  kubectl annotate pods --all env=prod name=norway
  #remove an annotation 
  kubectl annotate pods test-pod env-

  # Update a pod identified by the type and name in "pod.json"
  kubectl get pods test-pod -o yaml > pod.yaml
  kubectl annotate -f pod.yaml tube=victoria

```
