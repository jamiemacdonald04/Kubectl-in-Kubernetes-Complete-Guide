# kubectl expose
Lets talk about ports to help us understand what a service is.
**Port** exposes the Kubernetes service on the specified port within the cluster. 
**TargetPort** is the port on which the service will send requests to, that your pod will be listening on. 
**NodePort** exposes a service externally to the cluster by means of the target nodes IP address and the NodePort. 

## Environment

This is the starter for ten kubectl command.



```yaml
    # set up the environment
    kubectl create namspace media
    kubectl run books --image nginx -n media
    kubectl create deployment cds --image=nginx replicas=2 -n media
    kubectl create statefulset tapes --image=nginx replicas=2 -n media
    kubectl create rc stream --image=nginx replicas=2 --dry-run=client -o yaml -n media > stream.yaml

    # expose based on a deployment setting port and target port
    kubectl expose deploy cds --port=80 --target-port=8000 -n media
    kubectl get services -n media
    
    # expose based on a file definition
    kubectl expose -f stream.yaml --port=80 --target-port=8000 -n media
    kubectl get services -n media
    
    # choose a type  ClusterIP, NodePort, LoadBalancer, or ExternalName
    # give it a name
    kubectl expose statefulset tapes --port=444 --name=named-service --type='' -n media
    kubectl get services -n media
    
    # add a selecctor to the service 
    # add a label to the service
    kubectl expose pod books --labels='type=paperback' --selector='books' --port=444 -n media
    kubectl get services -n media


```
