# kubectl cluster information

Kubectl is used to create pods and is special in the right.  All other objects are created using kubectl create.

## Command

Arguments we are using.

```shell

# basic cluste info
k cluster-info 

# create a namespace
k create namespace test 

# create a deployment with 2 replicas
k create run first-app -n test--image nginx 

# see that pods are up
k get pods -n test

# use a dump to get the information you need
k cluster-info dump -n test -o yaml

# use grep to narrow down your search
k cluster-info dump -n test -o yaml | grep "kind: Pod"

# delete namespace and all objects
k delete namespace test


```
