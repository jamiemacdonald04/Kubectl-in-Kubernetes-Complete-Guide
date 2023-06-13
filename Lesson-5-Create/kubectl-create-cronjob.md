# kubectl create cronjob

## cronjob

Lets explore creating a cron job, schedule is 

``` shell
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │
# * * * * *

kubectl create cronjob my-cron-job1 --image=busybox --schedule="*/1 * * * *"
kubectl create cronjob my-cron-job2 --image=busybox --schedule="*/1 * * * *" -- sh -c "echo 'hello world!'" 
kubectl create cronjob my-cron-job3 --image=busybox --schedule="*/1 * * * *" --restart='OnFailure' # OnFailure or Never
kubectl create cj my-cron-job4 --image=busybox --schedule="*/1 * * * *" --dry-run=client -o yaml 
```
