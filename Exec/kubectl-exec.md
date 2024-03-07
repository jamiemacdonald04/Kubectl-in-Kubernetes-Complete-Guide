# kubectl exec

Kubectl exec is used to run commands on container within a pod.

## Command

Commands.

```shell

    k run shop --image nginx 

    # calls your method and then returns to your kubectl terminal
    k exec shop -t -- bash

    # allows you to add terminal commands but you dont see the prompt of either the kubectl or container terminal
    k exec shop -i -- bash

    # holds open a container terminal and shows input and output as if you where working on the terminal.
    k exec shop -it -- bash

    # so to run a one of command you can use the below statement,  I am listing the directories on the container in this case.
    # with or without the -t
    k exec shop -t -- printenv

    # do not add quotes to your command 
    k exec shop -it -- "ls --help"

    # command with arguments
    k exec shop -it -- ls --help

    # run multiple statements
    k exec shop -it -- ls && printenv

    # on a specific container 
    k exec shop -t -c shop-photos -- printenv

```

```YAML
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: shop
  name: shop
spec:
  containers:
  - image: redis
    name: shop-photos
    resources: {}
  - image: redis
    name: shop-front
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}


```
