# kubectl port-forward

The `kubectl port-forward` command is used to forward a port from a pod to your local machine.
This is a great way to access a service running in a pod without exposing it to the internet.
This will also allow you to use your local tools to interact with the service.

``` shell
kubectl create namespace starboard 
# default localhost and ip
kubectl create deployment shipping-website --port 80 --image nginx -n starboard 
kubectl expose deployment shipping-website --port 80 --target-port 80  -n starboard 
kubectl port-forward service/shipping-website 28015:80 -n starboard 

# any local ip
kubectl create deployment tanker-website --port 80 --image httpd  -n starboard 
kubectl expose deployment tanker-website --port 80 --target-port 80 -n starboard 
kubectl port-forward --address 0.0.0.0 service/tanker-website 28016:80 -n starboard 
curl 127.0.0.1:28016
curl 0.0.0.0:28016 

# random port and specific ip 
kubectl create deployment sailing-website --port 80 --image nginx -n starboard 
kubectl expose deployment sailing-website --port 80 --target-port 80 -n starboard 
# change port to have the name bob 
kubectl edit service sailing-website  -n starboard 
kubectl port-forward service/sailing-website --address localhost :bob -n starboard 
curl localhost:????
```
