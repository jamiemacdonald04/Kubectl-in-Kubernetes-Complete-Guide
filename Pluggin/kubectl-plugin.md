# kubectl plugin

The `kubectl plugin` command is used to manage kubectl plugins.   These are generally managed by third parties and are not part of the core kubectl command so buyer beware.

krew user guide
https://krew.sigs.k8s.io/docs/user-guide/

``` shell
kubectl plugin -h
kubectl plugin list 
# update 
kubectl krew update

# search
kubectl krew search

# search with keywords 
kubectl krew search pod

#get more information about a plugin
kubectl krew info tree

# pick one to install
kubectl krew install restart

# use the plugin 
kubectl restart -h
kubectl run dave --image=nginx 
kubectl restart dave

# uninstall the plugin 
kubectl krew uninstall restart
```
