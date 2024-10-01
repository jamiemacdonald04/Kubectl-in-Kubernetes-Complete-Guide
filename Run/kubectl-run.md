# kubectl Run

Kubectl run is a command that creates a pod.  You can use these pods to call out to other pods.  All other objects are created using methods like `kubectl create`, `kubectl expose` or `kubectl autoscale`.

## Command

Arguments we are using.

```shell
k run my-first-pod --restart=Never --command --labels="run=mypod,collection=gold" --annotations="collection=gold" --env="appName=tiger" --env="animal=tiger" --annotations="animal=tiger" --privileged  --image nginx --port=80 $dry -- sh -c "echo 'hello world'" > mypod
```

## YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    animal: tiger
    collection: gold
  creationTimestamp: null
  labels:
    collection: gold
    run: mypod
  name: my-first-pod
spec:
  containers:
  - command:
    - sh
    - -c
    - echo 'hello world'
    env:
    - name: appName
      value: tiger
    - name: animal
      value: tiger
    image: nginx
    name: my-first-pod
    ports:
    - containerPort: 80
    resources: {}
    securityContext:
      privileged: true
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
