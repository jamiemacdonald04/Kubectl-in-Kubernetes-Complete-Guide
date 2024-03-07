# kubectl Delete

Allows you to change add edit and delete labels on resources.

``` shell
# set up
k run barley --image nginx --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
k run corn --image nginx --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
k run wheat --image redis --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
k run rice --image nginx --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'
k run potato --image nginx --command -- bash -c 'for i in {1..10000}; do echo "Hi, $i"; sleep 1; done'

# give a pod a grace perod in time 
k delete pod corn --grace-period=1 -n default
# delete immedialty 
k delete pod wheat --force
# delete with minimal delay
k delete pod rice --now
# wait for finalizers
delete pod potato --wait 

# set up 
k create namespace farm
k create deploy fertaliser --image nginx -n farm
k run fuel --image nginx 
k create deploy pest-control --image nginx
k label deploy/pest-control pod/fuel farmers=supplies
k label deploy/fertaliser -n farm farmers=supplies

# delete all pods by label in all namespaces
k delete pods,deploy -l farmers=supplies -A

# set up 
k run four-by-four --image busybox 
k run tractor --image busybox

# delete all pods
k delete pods --all 

# delete muiltiple objects in one namespace
k run pitch-fork --image nginx
k expose pod pitch-fork --port 8089 
k delete pods,service pitch-fork 

# using a file 
k run combine-harvester --image nginx -o yaml --dry-run=client > pod.yaml 
k create -f pod.yaml 
k delete -f pod.yaml 

```