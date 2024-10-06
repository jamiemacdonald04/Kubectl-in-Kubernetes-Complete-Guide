# kubectl expose
The `kubectl expose` command is used to expose a resource through a new Kubernetes service.
**Port** exposes the Kubernetes service on the specified port within the cluster. 
**TargetPort** is the port on which the service will send requests to, that your pod will be listening on. 
**NodePort** exposes a service externally to the cluster by means of the target nodes IP address and the NodePort.

```shell
    # set up the environment
    kubectl create namespace media
    kubectl run books --image nginx -n media
    kubectl create deployment cds --image=nginx --replicas=2 -n media
    kubectl create deployment tapes --image=nginx --replicas=2 -n media
    kubectl create deployment stream --image=nginx --replicas=2 --dry-run=client -o yaml -n media > stream.yaml

    # expose based on a deployment setting port and target port
    kubectl expose deploy cds --port=80 --target-port=8000 -n media
    kubectl get services -n media
    
    # expose based on a file definition
    kubectl expose -f stream.yaml --port=80 --target-port=8000 -n media
    kubectl get services -n media
    
    # choose a type  ClusterIP, NodePort, LoadBalancer, or ExternalName
    # give it a name
    kubectl expose deployment tapes --port=444 --name=named-service --type='' -n media
    kubectl get services -n media
    
    # add a selecctor to the service 
    # expose all pods with this label.
    kubectl expose pod --labels='type=paperback' --selector="year=twentytwentyfour" --name=paperback-service --port=444 -n media
    kubectl get services paperback-service -n media --show-labels -o wide
    kubectl get pod books -n media --show-labels
    kubectl label pod books year=twentytwentyfour -n media


```
