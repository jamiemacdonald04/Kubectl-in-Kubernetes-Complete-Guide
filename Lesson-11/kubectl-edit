# Logs

## Environment

This is the starter for ten kubectl command.

```shell
# another pods for use with a selector filter "app". 
k run test-pod  --image nginx -l="app=another-app" --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
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

This is the sample yaml that will be edited in the second example of kubectl edit. We will see what can happen when you make changes that are not allowed and how to over come these.

```yaml
  containers:
  - name: write-logs #change here
    image: nginx
  - command:
    - bash
    - -c
    - for i in {1..10000}; do echo "Hi, $i"; sleep 1; done
    image: nginx
    imagePullPolicy: Always
    name: test-pod
    resources: {}
```

## Edit
Lets run the varaitions of the edit command.

``` shell
k edit pod test-pod 
k edit pod test-pod -o json
k edit pod test-pod --save-config
KUBE_EDITOR="nano" kubectl edit pod test-pod

```