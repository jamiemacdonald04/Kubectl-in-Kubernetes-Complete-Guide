# kubectl attach

kubectl attach is a convenient way to attach to a running container. It allows you to attach to the standard input, output, and error streams of a running container.

## Command

Commands to run in the terminal 

```shell
# create an example and connect to a default container
kubectl create namespace lochs
# stdin and tty are enabled by default for interactive containers, --attach argument is now set to true by default
kubectl run ness --image nginx -n lochs -i -t --command -- bash
kubectl attach pod ness -it -n lochs 
kubectl get pod ness -o yaml -n lochs

kubectl run leven --image nginx -n lochs --attach --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
kubectl attach pod leven -it -n lochs 

# laxford will be removed when the signal is given to quit the container 
kubectl run tay --rm --image nginx -n lochs -i -t --command -- bash -c 'for i in {1..10000}; do echo "Hello, $i"; sleep 1; done'

#create an example and connect to a specific container
kubectl run sween --image nginx -n lochs --command --dry-run=client -o yaml -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'  > sween.yaml
# add another container to the pod called villages
# see yaml below 
vim sween.yaml
kubectl apply -f sween.yaml
kubectl attach pod sween -it -n lochs -c sea

kubectl delete namespace lochs

```

Yaml to be added to the sween.yaml file
```yaml 
spec:
  containers:
  - command:
    - bash
    - -c
    - for i in {1..10000}; do echo "Goodbye, $i"; sleep 1; done
    image: nginx
    name: sea
```
