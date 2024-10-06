# kubectl set selector

The `kubectl set selector` command is used to set the selector on a resource.

```shell
# selector       
  # Set the selector on a resource
  kubectl create deployment bull-dog --image nginx
  kubectl label deployment bull-dog franky=said
  kubectl set selector deployment bull-dog franky=did-not-say

  kubectl create service nodeport bull-dog --tcp 8787
  kubectl get service/bull-dog -o wide 
  kubectl set selector service bull-dog franky=said
  kubectl get service/bull-dog -o wide 

```
