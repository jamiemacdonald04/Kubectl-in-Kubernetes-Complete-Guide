# kubectl Patch

The `kubectl patch` command is used to update fields in a resource.

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
# patch with files
k create deploy baker --image nginx

#save yaml below in patch.yaml
vim patch.yaml 
k patch deploy baker --type merge --patch-file patch.yaml 
k get pods 

vim patch2.yaml 
k patch deploy baker --type strategic --patch-file patch2.yaml 
k get pods 

k patch deploy baker --type merge --patch-file patch.yaml 
k get pods 


# patch with files
k create deploy butcher --image nginx --dry-run=client -o=yaml > patching-file.yaml
cat patching-file.yaml

k patch -f patching-file.yaml --local  --type merge --patch-file patch2.yaml -o yaml


```

```YAML
# file for patching, patch.yaml
spec:
  template:
    spec:
      containers:
      - name: patch1
        image: redis



# file for patching, patch2.yaml
spec:
  template:
    spec:
      containers:
      - name: patch2
        image: nginx
```
