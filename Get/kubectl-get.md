# kubectl Get

## Environment

Lets set up the ksql get environment

```shell

kubectl api-resources -owide | grep get -m20

kubectl create namespace shop-area 
kubectl create deployment shop-woolies --image redis -n shop-area 
kubectl create deployment shop-wilkos --image redis -n shop-area 
kubectl expose deployment shop-wilkos --port 8080 -n shop-area 
kubectl create cronjob shop-inventry --image nginx --schedule="* * * * 1" -n shop-area 

# working with labels 
kubectl label deployment shop-woolies woolworths=dundee  -n shop-area 
kubectl get deployments --show-labels  -n shop-area 
kubectl get deployment -l woolworths=dundee -n shop-area 

# SHOW KIND
kubectl get pods --show-kind -n shop-area 

# NO ERROR
# do not through an erro if a resource is not found 
 kubectl get pods warehouse -n shop-area --ignore-not-found

# NO HEADERS
# kubectl get without the headers 
kubectl get deployments --no-headers -n shop-area 

# ALL NAMESPACES
# view all namespaces and on label
kubectl get deployment -l woolworths=dundee -A 

# OUTPUT
# viewing yaml using output
kubectl get cronjob shop-inventry -o yaml  -n shop-area 
kubectl get cronjob shop-inventry -o json  -n shop-area 
kubectl get deploy -o wide -n shop-area 

# get a containers name 
kubectl run shop-cafe --image nginx   -n shop-area 
# add another container 
kubectl edit pod shop-cafe    -n shop-area 
# output container names
kubectl get pod/shop-cafe -o jsonpath={.spec.containers[*].name}   -n shop-area && echo
# experiment with json path 
#https://jsonpath.com/

# sort by name 
kubectl run alphabet-toys --image nginx -n shop-area 
kubectl get pods --sort-by='{.metadata.creationTimestamp}' -n shop-area 

# CUSTOM COLUMNS
# 100% custom colums
kubectl get pods  -o custom-columns="POD NAME":.metadata.name,"CONTAINER NAME":.spec.containers[*].name,"CONTAINER IMAGE":.spec.containers[*].image -n shop-area 

# WATCH
# add a watch and watch only 
kubectl create deployment shop-fitters -n shop-area  --image nginx --replicas 6 && kubectl get pods --watch -n shop-area 

kubectl create deployment shop-marketing -n shop-area --image nginx --replicas 6 && kubectl get pods --watch-only -n shop-area 

kubectl create deployment shop-facilites --image nginx --replicas 6 && kubectl get pods --watch-only --output-watch-events=true -n shop-area 

# PRINT SERVER
# server print default and off (without age status and restarts)
kubectl get pods --server-print=false

# GET POD BASED ON RESOURCES IN A FILE
# get a pod content by using the file command, will only display if it is there
kubectl run corner-shop --image nginx -o yaml --dry-run=client > cornershop.yaml
kubectl get -f cornershop.yaml
kubectl apply -f cornershop.yaml
kubectl get -f cornershop.yaml


# MORE THAN ONE RESOURCE TYPE
# get a few resources at once
kubectl get deployment/shop-woolies cronjob/shop-inventry pods/corner-shop services/shop-wilkos -n shop-area 
kubectl get services,deployment,cronjob,pod -n shop-area 

# MULTIPLE TO FILE
# output it to a file (namespaces are a global resource)
kubectl get services,deployment,cronjob,pod -n shop-area -o yaml > file.yaml
cat file.yaml 
kubectl get -f file.yaml

# get all resources for a namespace 
kubectl get all -n shop-area

#HIDDEN RESOURCES
# get hidden resources 
kubectl create ingress shops --rule="shops.com/service=shop:8080" -n shop-area
kubectl api-resources --verbs=list --namespaced -o name | head -n 20
kubectl api-resources --verbs=list --namespaced -o name | xargs -n1 kubectl get --show-kind --ignore-not-found -n shop-area 

  # for those extra large lists 
kubectl get all -n shop-area --chunk-size=500

```
