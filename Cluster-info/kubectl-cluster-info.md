# kubectl cluster information

The `kubectl cluster-info` command is used to get the information about the cluster.  
This is useful when you want to know the status of the cluster and the services that are running.

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
