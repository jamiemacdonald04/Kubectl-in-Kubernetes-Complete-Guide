# kubectl create job

## job

Edited YAML.

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: test-job
spec:
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - command:
        - sh
        - -c
        - echo "hello world, ${rest}"
        env:
        - name: rest
          value: "Is the weather ok?"
        image: nginx
        name: test-job
        resources: {}
      restartPolicy: Never
status: {}
```

Lets explore creating a job

``` shell
kubectl create job my-job1 --image=busybox
kubectl create job my-job2 --image=busybox -- sh -c "echo 'hello world!'" 
kubectl create job my-job4 --image=busybox --dry-run=client -o yaml 
kubectl create job my-job4 --from cronjob/my-cron-job1

```