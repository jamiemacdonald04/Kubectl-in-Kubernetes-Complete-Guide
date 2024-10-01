# kubectl autoscale
The `kubectl autoscale` command is a declarative command that will create a horizontal pod autoscaler for a resource in your cluster.
You can use the `--cpu-percent` flag to set the CPU utilization target for the autoscaler.
    
```shell
# set up metrics 
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl -n kube-system edit deployments.apps metrics-server
#edit with yaml below


kubectl create namespace wwe 
kubectl create deploy big-show --replicas 1 --image registry.k8s.io/hpa-example --port 80 -n wwe
kubectl set resources deployment big-show --requests=cpu=200m --limits=cpu=500m -n wwe
kubectl expose deploy big-show --port=80 -n wwe
kubectl autoscale deployment big-show --cpu-percent=50 --min=1 --max=10 -n wwe
kubectl get hpa -n wwe

# bacl in the first tab run the following command
kubectl run -i --tty load-generator --rm --image=busybox:1.28 -n wwe --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://big-show; done"



```
```yaml 
command:
- /metrics-server
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP

```
