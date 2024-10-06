# kubectl set image

The `kubectl set image` command is used to update the image of a container in a pod. 

```shell
# images
  # Set a deployment's nginx container image to 'nginx:1.9.1', and its busybox container image to 'busybox'
  kubectl create deploy kitchen --image nginx
  kubectl edit deploy kitchen
  kubectl set image deployment kitchen redis=redis nginx=nginx:1.9.1
  
  # Update all deployments nginx container's image to 'nginx:1.9.1'
  kubectl set image deployments nginx=nginx --all
    kubectl set image deployments nginx=nginx:1.9.1 --all
  
  # Update image of all containers of a deploymet to 'redis'
  kubectl set image deployments kitchen *=redis
  
  # Print result (in yaml format) of updating nginx container image from local file, without hitting the server
  kubectl create deployment living-room --image redis  -o yaml --dry-run=client > deploy.yaml 
  kubectl set image -f deploy.yaml redis=nginx:1.9.1 --local -o yaml > deploy2.yaml
```
