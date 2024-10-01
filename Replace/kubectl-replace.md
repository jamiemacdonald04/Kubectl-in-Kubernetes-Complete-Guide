# kubectl replace
The `kubectl replace` command is a declarative command that will replace the configuration defined in files to your cluster.
You can force the replacement of the resource by using the `--force` flag.

```shell
# set up the environment
kubectl create namespace musical-instruments
kubectl run guitar --image=nginx --dry-run=client -n musical-instruments -o yaml > guitar.yaml
kubectl create deploy violin --image=nginx --dry-run=client -n musical-instruments -o yaml > violin.yaml
kubectl create deploy piano  --replicas=30 --image=nginx --dry-run=client -n musical-instruments -o yaml  -- bash -c 'for i in {1..10000}; do echo "key counter, $i"; sleep 1; done' > piano.yaml
kubectl apply -f guitar.yaml 
kubectl apply -f violin.yaml
kubectl apply -f piano.yaml
kubectl get pods -n musical-instruments

# Replace a pod using the data in pod.json
kubectl replace -f ./guitar.yaml
kubectl replace --force -f ./guitar.yaml

# edit the file and replace the pod
vim violin.yaml 
cat violin.yaml | kubectl replace -f -

# allow graceful shutdown of the pod before replacing
kubectl replace -f piano.yaml --grace-period=30 --force 
# only possible if the force flas is used 
kubectl replace --force -f piano.yaml --grace-period=0
```


