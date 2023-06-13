# kubectl Patch

## Environment

This is the starter for ten kubectl command.

```shell
# run a pod ready for patching
k run test-pod  --image nginx -l="app=another-app" 

```

## Patches yaml

``` yaml

metadata:
  creationTimestamp: null
  labels:
    app: test-container

```

## Patch Commands

Lets run commands to get logs based on all containers, a single container, a deployment (gotcha), with a selector, identifiers and more.

``` shell
k patch pod test-pod --type merge -f 
k patch pod test-pod --type replace -f 

k patch pod test-pod --type merge -p '{"spec":{"metadata":{"labels": [{"new":"label"}]}}}'
k patch pod test-pod --type replace -p '{"spec":{"metadata":{"labels": [{"new":"label"}]}}}'
```