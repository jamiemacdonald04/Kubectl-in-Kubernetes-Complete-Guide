# Logs

## Environment

This is the starter for 10 kubectl command.

```shell
# a deployment 
k create deploy test-container  --image nginx  --replicas 6  -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done' > deploy.yaml

# edit as below yaml and then 
k apply -f deploy.yaml

# another pods for use with a selector 
k run test-pod  --image nginx -l="app=another-app" --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
```

This is the edited yaml for our environment.  Notice it has two containers.

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
All Conatiners

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