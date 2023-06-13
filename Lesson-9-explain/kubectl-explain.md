# Kubectl Explain

## Environment

This is the starter for ten kubectl command.

```shell
# another pods for use with a selector filter "app". 
k run test-pod --image nginx $dry > pod.yaml 
k create configmap furniture --from-literal="oak=table" 

```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: test-pod
  name: test-pod
spec:
  containers:
  - image: ubuntu:latest # change for debug  
    command:
    - bash
    - -c
    - sleep 500
    envFrom:
    - configMapRef: # change for syntax changing
       name: furniture
    name: test-pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Explain and grep

Let's use the explian kubectl command to get clues how to format our yaml.

``` shell
k explain pod 
k explain pods.spec
k explain pods.spec.volumes.secret
k explain pods.spec.volumes.secret --recursive

k explain pod --recursive | grep -iA20 -B20 envfrom

k exec test-pod -it -- bash # to check the env var is present

```
