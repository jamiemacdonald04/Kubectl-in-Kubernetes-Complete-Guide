# kubectl create namespace

The `kubectl create namespace` command is used to create a namespace in the cluster.  
A namesapce is a way to divide cluster resources between multiple users and workspaces, also it is a way to create a virtual cluster within the cluster.

```yaml

apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: null
  name: choco
spec: {}
status: {}
---
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: sprinkes
  name: sprinkes
  namespace: choco
spec:
  containers:
  - image: nginx
    name: sprinkes
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```

## namespace

Lets explore creating a namespace

``` shell
kubectl create namespace choco --dry-run=client -o yaml
kubectl create namespace choco
k run sprinkes --image=nginx -n choco $dry 
kubectl get pods -n choco
kubectl delete pods sprinkes -n choco
kubectl delete namespace choco

kubectl api-resources --namespaced=false
kubectl api-resources --namespaced=true

```
