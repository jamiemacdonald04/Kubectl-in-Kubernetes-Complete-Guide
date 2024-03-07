# kubectl taint

Kubectl drain is used to manage the move of pods from one node to another.

## Command

Commands.

```shell
  # explore help 
  kubectl taint -h 

  # add taint node 
  kubectl taint nodes minikube user=jamie:NoSchedule

  # lets take a look at it 
  kubectl get node minikube -o yaml

  # create a pod and try and schedule it 
  k run pod dave --image nginx 
 
  # remove the taint 
  kubectl taint nodes minikube -user


```

```YAML
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: dave
  name: dave
spec:
  containers:
  - image: redis
    name: shop-photos
    resources: {}
  tolerations:
  - key: "user"
    operator: "jamie"
    effect: "NoSchedule"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}


```
