# kubectl create deployment

## deployment

Lets explore creating a deployment

``` shell
k create deployment test-deployment --image nginx --replicas 3 --port 5701  --dry-run=client -o yaml -- ssh -c "echo 'hello world'; sleep 5000" > test-deployment.yaml

k create deployment -f test-deployment.yaml
```

The yaml after we edited it via vim editor.

```yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test-deploy
  name: test-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: test-deploy
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test-deploy
    spec:
      containers:
      - name: logging-container
        image: nginx
        env:
        - name: admin
          value: "true"
      - command:
        - sh
        - -c
        - echo 'hello world'; sleep 5000
        image: nginx
        name: main-container
        ports:
        - containerPort: 5326
        resources: {}
status: {}

```
