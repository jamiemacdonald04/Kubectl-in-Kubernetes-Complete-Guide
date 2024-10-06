# kubectl set

The `kubectl set resources` command is used to set resource requests and limits on a resource. 

```shell

# resources
  # defining one container only      
  kubectl create deploy poodle --image nginx
  kubectl set resources deployment poodle -c=nginx --limits=cpu=200m,memory=512Mi
  kubectl describe deployment poodle
  
  # Set the requested and the limit of resources that can be used for all containers.
  kubectl set resources deployment poodle --limits=cpu=200m,memory=512Mi --requests=cpu=100m,memory=256Mi
  kubectl describe deployment poodle
  
  # Remove the resource requests for resources on containers in nginx
  kubectl set resources deployment poodle --limits=cpu=0,memory=0 --requests=cpu=0,memory=0
  kubectl describe deployment poodle
  
  # Print the result (in yaml format) of updating nginx container limits from a local, without hitting the server
  kubectl create deployment dalmation --image redis  -o yaml --dry-run=client > deploy.yaml 
  kubectl set resources -f deploy.yaml --limits=cpu=200m,memory=512Mi --local -o yaml > deploy2.yaml
```
