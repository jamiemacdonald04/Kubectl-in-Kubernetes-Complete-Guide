# kubectl diff

The `kubectl diff` command is used to compare the differences between the current state of an object and the desired state of an object.

``` shell

# lets make a script that we can pretend we have had lying around and has been stored a while in GitHub.
k run  live-pod --dry-run=client -o yaml  --image nginx -- sh -c "echo 'jamie'" > stored-pod.yaml

# now lets create a pod that we are intersted in testing the stored script above.
k run  live-pod --image nginx --command  -- sh -c "echo 'jamie'" 

# use diff to see the differences. 
kubectl diff -f stored-pod.yaml

# for retro fitting creation statements.
kubectl run  live-pod --image nginx -o yaml --dry-run=client  -- sh -c "echo 'jamie'" | kubectl diff -f -
kubectl run  live-pod --image nginx -o yaml --dry-run=client --command  -- sh -c "echo 'jamie'" | kubectl diff -f -

# a pod that compares to nothing.
kubectl run newpod --image nginx  -o yaml --dry-run=client  | kubectl diff -f -
```
