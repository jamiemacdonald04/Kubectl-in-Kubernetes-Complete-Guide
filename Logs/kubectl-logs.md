# kubectl Logs

The `kubectl logs` command is used to print the logs from a container in a pod. 

```shell
# a deployment 
kubectl create deploy test-pod  --image nginx  --replicas 6  -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done' > deploy.yaml

# edit as below yaml and then 
kubectl apply -f deploy.yaml

# another pods for use with a selector filter "app". 
kubectl run test-pod  --image nginx -l="app=another-app" --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
```

This is the edited yaml for our environment from the first create statement edited in vim.  Notice it has two containers, one with hello world and one with hello moon printed in logs.

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test-container
  name: test-container
spec:
  replicas: 6
  selector:
    matchLabels:
      app: test-container
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test-container
    spec:
      containers:
      - name: first-container
        image: nginx
        command:
        - bash
        - -c
        - for i in {1..10000}; do echo "Hello Moon $i"; sleep 1; done
      - command:
        - bash
        - -c
        - for i in {1..10000}; do echo "Hello World $i"; sleep 1; done
        image: nginx
        name: second-container
        resources: {}
status: {}
```

## Logs 
Lets run commands to get logs based on all containers, a single container, a deployment (gotcha), with a selector, identifiers and more.

``` shell
k logs test-container-[pod unique id] --all-containers
k logs test-container-[pod unique id] --all-containers --follow
k logs test-container-[pod unique id] --c first-container

# only shows one pod.
k logs deploy/test-container --all-containers -f 
k logs deploy/test-container --all-containers -f --tail=20 

# shows all pods with selector
k logs -l "app=test-container"  --max-log-requests=6
k logs -l "app=test-container" --prefix --timestamps --max-log-requests=6 --follow 
k logs -l "app=test-container" --prefix --timestamps --since 5s
k logs -l "app=test-container" --since-time=2023-05-31T20:03:50.122512000Z 

k logs -l "app=" --prefix --timestamps --max-log-requests=7 --follow 
```
