# kubectl create serviceaccount

The `kubectl create serviceaccount` command is used to create a service account object in the cluster.

## serviceaccount

lets explore creating a service account

Generated yaml.

```yaml

apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2023-11-11T11:41:56Z"
  name: call-sa
  namespace: default
  resourceVersion: "373773"
  uid: 075f926f-7eb9-43c0-9c07-37a179e2a4bf
secrets:
- name: call-sa-token-mmcwm

```

``` shell
# create a deployment with kubectl pre installed
k create deploy dep-caller --image bitnami/kubectl -- sh -c 'kubectl get pods'

# look at logs 
k logs dep-caller[unique code]

# find out what verbs you want to use.
k api-resources -o wide | grep pods

# create a role with permission to list get and watch pods.
kubectl create role role-sa --verb=get,list,watch --resource=pods,pods/status 

# create a service account 
kubectl create serviceaccount call-sa

# create a rolebindng
kubectl create rolebinding admin --serviceaccount=default:call-sa --role=role-sa

# add service account to deployment using set 
kubectl set serviceaccount deployment dep-caller  call-sa

# look at logs of the new pod created as a result of the service account being updated.
k logs dep-caller[unique code]

# lets jump on to the pod and have a look around 
k exec dep-caller[unique code] -it --sh


```
