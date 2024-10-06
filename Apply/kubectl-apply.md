# kubectl apply
The `kubectl apply` command is a powerful command that is used to apply configuration to your kubernetes cluster.
You will use this a lot to apply yaml to your kubernetes cluster.  
It is a powerful command that can be used to create and update resources in your cluster.  
It is a declarative command that will apply the configuration defined in files to your cluster.
It can also be used to see last configuration applied to a resource.

```shell
# environment set up
mkdir bike-shop && cd bike-shop 
kubectl create namespace bikes

# create a pod in the bikes namespace in yaml
kubectl run fast-bikes --image=nginx --dry-run=client -n bikes -o yaml > fast.yaml 
kubectl apply -f fast.yaml
kubectl get pods -n bikes 

# namespace on the apply statement 
kubectl run slow-bikes --image=nginx --dry-run=client -o yaml > slow.yaml 
kubectl apply -f slow.yaml -n bikes
kubectl get pods -n bikes 

# clean down 
kubectl delete pods --all -n bikes
kubectl get pods -n bikes

# run multiple commands in one line
ls
kubectl apply -f '*.yaml' -n bikes

#add a label to the pod.yaml before applying 
kubectl run fat-bikes --image=nginx --dry-run=client -n bikes -o yaml \
| kubectl label -f -  status=unhealthy -o yaml --dry-run=client --local=true | kubectl apply -f -
kubectl get pod fat-bikes -n bikes --show-labels

# create a file with multiple resources
kubectl get pods fat-bikes -n bikes -o yaml  > manifest.yaml && \
echo "---" >> manifest.yaml

kubectl run montain --image=nginx --dry-run=client -n bikes -o yaml \
| kubectl label -f -  status=healthy -o yaml --dry-run=client --local=true  >> manifest.yaml && \
echo "---" >> manifest.yaml

kubectl run racer --image=nginx --dry-run=client -o yaml \
| kubectl label -f -  status=healthy -o yaml --dry-run=client --local=true >> manifest.yaml

# lets change based on label
kubectl apply -f manifest.yaml -n bikes
vim manifest.yaml # add new labels to the resources
kubectl get -f manifest.yaml -n bikes --show-labels
kubectl apply -f manifest.yaml -l status=healthy -n bikes
kubectl get -f manifest.yaml --show-labels -n bikes


# lets prune objects that we dont want changes to happen to
kubectl get -f manifest.yaml -n bikes --show-labels
vim manifest.yaml # remove fat bikes
kubectl apply --prune --prune-allowlist=core/v1/Pod -f manifest.yaml --all -n bikes
kubectl get -f manifest.yaml --show-labels -n bikes

# touch breifly on kustomize
curl -s -o "#1.yaml" "https://raw.githubusercontent.com\
/kubernetes-sigs/kustomize\
/master/examples/helloWorld\
/{configMap,deployment,kustomization,service}.yaml"
kubectl apply -k . -n bikes
kubectl get pods,services,configmap -n bikes
kubectl delete -k . -n bikes

# edit the last applied configuration, lets edit the container name
kubectl apply edit-last-applied -n bikes -f manifest.yaml
kubectl get pods -n bikes --show-labels
kubectl get pods fat-bikes -n bikes -o yaml

# view the last applied configuration
kubectl apply view-last-applied  -n bikes pod  fat-bikes 
# set the last applied configuration to that of the original manifest
kubectl apply set-last-applied -n bikes -f manifest.yaml
kubectl apply view-last-applied  -n bikes -f manifest.yaml

# clean up
k delete namespace bikes
cd ../ && rm -r bike-shop

```
