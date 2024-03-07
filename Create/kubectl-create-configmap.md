# kubectl create configmap

Edited test yaml for pod using configMaps
```yaml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: test-pod
  name: test-pod
spec:
  volumes: # This is what loads the config map into a volume ready to be consumed by containers.
  - name: slogan
    configMap:
      name: ice-cream-shop-slogan
  containers:
  - image: nginx
    name: test-pod
    envFrom: # addding all key value pairs named as they are in the config map
    - configMapRef:
       name: ice-cream-shop-settings
    env: #adding single key value pair with different name
    - name: ICECREAM
      valueFrom: # setting the drive on the container to have the volume specified above
        configMapKeyRef:
          name: ice-cream-shop-settings
          key: defaultIceCream
    volumeMounts:
    - name: slogan
      mountPath: slogan
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

## configmap

Lets explore creating a config map

``` shell
  echo -e "defaultIceCream=vanilla\ndefaultTopping=flake\ndefaultCandy=Space-hoppers" > testFile1.env
  echo -e "I once went for a walk on the beach"  > testFile2.env
  
  # adding files
  k create configmap ice-cream-shop-slogan --from-file=testFile2.env $dry
  kubectl create configmap my-config --from-file=key1=testFile1.env --from-file=key2=testFile2.txt
  
  # individual values added manually
  kubectl create configmap my-config-individual --from-literal=username=user1 --from-literal=password=password123

  # individual values from a file
  k create configmap ice-cream-shop-settings --from-env-file=testFile1.env

```
