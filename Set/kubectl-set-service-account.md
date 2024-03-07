# kubectl set 

## Environment

Lets expore setting a service account for a container

```shell
  # serviceaccount Update the service account of a resource
  kubectl create deployment shitsu --image nginx 
  kubectl create serviceaccount doggy
  kubectl set serviceaccount deployment shitsu doggy
  kubectl describe deployment shitsu
  
  kubectl create deployment german-shepard --image nginx --dry-run=client -o yaml > deploy.yaml
  kubectl set serviceaccount -f deploy.yaml doggy --local --dry-run=client -o yaml

```
