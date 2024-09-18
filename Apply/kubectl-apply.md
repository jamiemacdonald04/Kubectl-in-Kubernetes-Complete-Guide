# kubectl apply
Let's explore the kubectl apply command in great detail.

```shell
# environment set up
mkdir bike-shop
cd bike-shop 
kubectl create namespace bikes

# create a pod in the bikes namespace in yaml
kubectl run fast-bikes --image=nginx --dry-run=client -n bikes -o yaml > pod1.yaml 
kubectl apply -f pod1.yaml

# namespace on the apply statement 
kubectl run slow-bikes --image=nginx --dry-run=client -o yaml > pod2.yaml 
kubectl apply -f pod2.yaml -n bikes

# clean down 
kubectl delete pods --all -n bikes
kubectl get pods -n bikes

# run multiple commands in one line
kubectl apply -f '*.yaml' -n bikes

#add a label to the pod.yaml before applying 
kubectl run fat-bikes --image=nginx --dry-run=client -n bikes -o yaml \
| kubectl label -f -  status=unhealthy -o yaml --dry-run=client --local=true | kubectl apply -f -
kubectl get pod fat-bikes -n bikes --show-labels

# create a file with multiple resources
kubectl get pods fat-bikes -n bikes -o yaml  > manifest.yaml
echo "---" >> manifest.yaml
kubectl run montain --image=nginx --dry-run=client -n bikes -o yaml \
| kubectl label -f -  status=healthy -o yaml --dry-run=client --local=true  >> manifest.yaml
echo "---" >> manifest.yaml
kubectl run racer --image=nginx --dry-run=client -o yaml \
| kubectl label -f -  status=healthy -o yaml --dry-run=client --local=true >> manifest.yaml

kubectl apply -f manifest.yaml -n bikes
kubectl get -f manifest.yaml
kubectl apply --prune --prune-allowlist=core/v1/Pod -f manifest.yaml -l status=healthy -n bikes
kubectl get -f manifest.yaml


curl -s -o "#1.yaml" "https://raw.githubusercontent.com\
/kubernetes-sigs/kustomize\
/master/examples/helloWorld\
/{configMap,deployment,kustomization,service}.yaml"
kubectl apply -k . -n bikes
kubectl get pods,services,configmap -n bikes
kubectl delete -k . -n bikes

# edit the last applied configuration, lets edit the container name
kubectl apply edit-last-applied -n bikes -f manifest.yaml
kubectl get pods -n bikes 
kubectl apply view-last-applied  -n bikes -f manifest.yaml
kubectl apply set-last-applied -n bikes -f manifest.yaml
kubectl apply view-last-applied  -n bikes -f manifest.yaml

```
