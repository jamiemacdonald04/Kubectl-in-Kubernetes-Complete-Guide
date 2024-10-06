# kubectl proxy

The `kubectl proxy` is a command that is used to create a proxy server between your machine and the Kubernetes API server. 
This is useful when you want to access the Kubernetes API server directly.

``` shell
# http://127.0.0.1:57239/api/v1/namespaces/default/pods
# kubectl proxy --port=0
# https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/#directly-accessing-the-rest-api
```
