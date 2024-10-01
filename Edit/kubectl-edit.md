# Kubectl Edit

The `kubectl edit` is a command that is used to edit the configuration of a resource in the cluster. 
This is useful when you want to make changes to a resource that is already running in the cluster. 

```shell
# another pods for use with a selector filter "app". 
k run test-pod  --image nginx --command -- bash -c "sleep 500"

k create deploy test-deploy --image nginx -- bash -c "sleep 500"
```

This is the sample yaml that will be edited in the first example of kubectl edit.

``` yaml
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2023-06-01T19:47:12Z"
  labels:
    app: another-app
    first: example # changes here 
  name: test-pod
  namespace: default
```

This is the sample yaml that will be edited in the second example of kubectl edit. We will see what can happen when you make changes that are not allowed and how to over come these.  First in the pod where it is allowed and then in the deploy where it is not allowed.

```yaml
  containers:
  - name: ubumtu 
    image: ubuntu:latest #change here
    imagePullPolicy: Always
    name: test-pod
    resources: {}
```

Also what do we do if we get an error.

```yaml
  containers:
  - name: ubumtu 
    image: ubuntu:latest 
    imagePullPoliy: Always #change here
    name: test-pod
    resources: {}
```

## Edit
Lets run the varaitions of the edit command.

``` shell
k edit pod test-pod 

# used to find out the history after image change.
k rollout history pod test-pod

# used when trying to change the restart policy inside the container of the pod.
k replace -f "temp file displayed by terminal" --force

k edit pod test-deploy 
k edit pod test-pod -o json
k edit pod test-pod --save-config

KUBE_EDITOR="nano" kubectl edit pod test-pod

```
