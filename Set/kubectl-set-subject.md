# kubectl set subject

The `kubectl set subject` command is used to update the user, group, or service account in a role binding or cluster role binding.

```shell
# subject        
  #Update the user, group, or service account in a role binding or cluster role binding
  kubectl create rolebinding petstore --clusterrole=admin --user=user1 --group=group1
  k get rolebinding petstore -o wide
  kubectl set subject rolebinding petstore --user=user1 --user=user2 --group=group1
  k get rolebinding petstore -o wide
```
