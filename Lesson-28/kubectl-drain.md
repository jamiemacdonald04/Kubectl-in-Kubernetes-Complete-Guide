# kubectl drain

Kubectl drain is used to manage the move of pods from one node to another.

## Command

Commands.

```shell
k drain -h 

# create a deployment 
k create deploy shop --image nginx --replicas 2

# check out what nde it is on
k get pods -o wide

# drain node and ingnore deamonsets 
k drain node01 --ignore-daemonsets

# get the nodes and see that it has ben cordoned
k get nodes 

# see how pods have come down and moved to the controlpane node
k get pods -o wide

# uncordon the node  
k uncordon node01

# refer to lecture, how to add a static volume. yaml below.
k run shop-photos --image redis --dry-run=client -o yaml > pod.yaml

# create pod 
k apply -f pod.yaml 

# check out what node it is on
k get pods -o wide

# force deletion of pod as it has no controller or eviction methodoligy and also delete it regardless of its static drive 
k drain node01 --delete-emptydir-data=false --ignore-daemonsets --force

```

```YAML
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: shop-photos
  name: shop-photos
spec:
  volumes:
  - name: photos
    emptyDir: {}
  containers:
  - image: redis
    name: shop-photos
    resources: {}
    volumeMounts:
    - mountPath: /photos
      name: photos
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}


```
