# kubectl auth can i

Kubectl is used to determine if you user can or cannot do a certain action

## Command

Arguments we are using.

```shell
  kubectl   api-resources -o wide 
  # can i list pods
  kubectl auth can-i create pods 

  # can i list deployments
  kubectl auth can-i list deployments
  
  # Check to see if service account "sandy" of namespace "sandy-beaches" can list pods
  # in the namespace "peable-beaches".
  # of course we cannot do this as we have not added the sa to a role with permissions
  kubectl create namespace sandy-beaches 
  kubectl create namespace peable-beaches 
  kubectl create sa sandy
  kubectl create sa peables 
  kubectl auth can-i list pods --as=system:serviceaccount:sandy:sandy-beaches  -n peable-beaches
  
  # check if i can do all verbs and all types (so everything)
  kubectl auth can-i '*' '*'
  
  # Intersting that this job does not exits but in thoery it allows it
  kubectl auth can-i list/jobs bar -n foo
  
  # can i get a sub resource for example logs in a pod
  kubectl auth can-i get pods --subresource=log
  
  # List all allowed actions in all namespaces 
  kubectl auth can-i --list 
  
  # without headers 
  kubectl auth can-i --no-headers  --list

  # invalid 
  kubectl auth can-i --no-headers  --list -A

  # complete with a success code only 
  kubectl auth can-i list jobs/bar -n foo -q

```
