# kubectl rollout 
The `kubectl rollout` allows you to manage the rollout of a deployment. You can use the `kubectl rollout` command to view the status of a deployment, pause a deployment, resume a deployment, and undo a deployment.
```shell
# set up the environment
kubectl create namespace europe
kubectl create deployment ireland --image nginx -n europe
kubectl rollout status deploy ireland -n europe


kubectl rollout history deploy ireland -n europe
# container name then image name you want to change
kubectl set image deploy ireland nginx=nginx:1.16.1 -n europe
kubectl rollout status deploy ireland -n europe
kubectl rollout history deploy ireland -n europe
kubectl annotate deploy ireland -n europe kubernetes.io/change-cause="specific version of nginx"
kubectl rollout history deploy ireland -n europe
kubectl set image deploy ireland nginx=nginx:busybox -n europe
kubectl annotate deploy ireland -n europe kubernetes.io/change-cause="specific version of busybox"

# exploring revisions 
kubectl rollout history deploy ireland --revision=2 -n europe
kubectl rollout history deploy ireland --revision=2 -o yaml -n europe
kubectl rollout history deploy ireland --revision=3 -o yaml -n europe

# undoing rollouts 
kubectl set resources deployment ireland --limits=cpu=200m,memory=512Mi --requests=cpu=100m,memory=256Mi -n europe
kubectl annotate deploy ireland kubernetes.io/change-cause="resource limits and requets" -n europe
kubectl rollout history deploy ireland -n europe
kubectl rollout undo deploy ireland -n europe
kubectl rollout history deploy ireland -n europe
kubectl set resources deployment ireland --limits=cpu=200m,memory=512Mi --requests=cpu=100m,memory=256Mi -n europe
kubectl annotate deploy ireland kubernetes.io/change-cause="resource limits and requets" -n europe
kubectl rollout undo deploy ireland -n europe --to-revision=2
kubectl rollout history deploy ireland -n europe

# pause and resume rollouts
kubectl edit deploy ireland -n europe
#change the replicas to 20
kubectl rollout status deploy ireland -n europe
kubectl set image deploy ireland nginx=nginx -n europe
kubectl rollout status deploy ireland -n europe
kubectl rollout pause deploy ireland -n europe
kubectl rollout resume deploy ireland -n europe

#restart a rs
kubectl rollout restart deploy ireland -n europe

```


