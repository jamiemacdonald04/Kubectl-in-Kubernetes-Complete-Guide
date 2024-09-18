# kubectl describe

Kubectl is used to describe the definition of kubernetes resources

## Command

Arguments we are using.

```shell

# lets create some test resources
kubectl run jeansco-front-end --image=nginx 
kubectl run jeansco-backend-end --image=nginx 
kubectl run jeansco-database --image=nginx 
kubectl run jeansco-cache --image=sdfasfsadfas 

# look at events to find out why it failed
kubectl describe pod jeansco-cache

#based on name
kubectl describe pod jeansco-backend-end
kubectl describe pod  jeansco-backend-end | grep Port:

# prefixk 
kubectl describe pod jeansco
kubectl describe pod jeansco | grep -w  Name: 

# with label
kubectl label pod jeansco-database type=mysql 
kubectl describe pod -l type=mysql
kubectl describe pod -l type=mysql | grep -w  Name: 

# based on a file 
kubectl get pod jeansco-front-end -o yaml > jeansco.yaml
kubectl describe -f jeansco.yaml 

# do not show the events that have happened
kubectl describe pod jeansco-backend-end
kubectl describe pod jeansco-backend-end --show-events=false 

# does not work
kubectl create namespace entertainment
kubectl run jeansco-api --image=nginx -n entertainment
kubectl describe pod jeansco -A | grep -w  Name: 
kubectl describe pod -A | grep -w  Name: 
kubectl describe pod -A | grep -w  Name: | grep jeansco


```
