# kubectl cp

## Environment

We look into copying files from the computer to the server


```shell
    # set up and add another container, see the yaml below
    kubectl run shop --image nginx
    kubectl edit pod shop 
    kubectl exec shop  -- tar
  

    # copy a file from your computer to pods container
    echo "hello" > hello.txt
    kubectl cp ./hello.txt shop:/tmp/hello.txt -c shop-photos
    kubectl exec shop  -c shop-photos -- cat ./tmp/hello.txt


    # create a new file on the pod and copy it to this pc
    kubectl exec shop -c shop-front -it -- bash
    cd ../ && cd ./tmp && mkdir goodbye && cd goodbye && echo "goodbye" > goodbye.txt
    kubectl cp shop:/tmp/goodbye.txt ./goodbye.txt -c shop-front 
    ls 

    # lets copy a directory 
    mkdir toolbox && cd toolbox
    echo "hammer" > hammer.txt && echo "screw driver" > screw_driver.txt && echo "spanner" > spanner.txt
    cd ../
    kubectl cp ./toolbox shop:/tmp/tooolbox  -c shop-photos --no-preserve=false
    kubectl exec shop  -c shop-photos -- ls ./tmp/tooolbox

    # from one pod to another (check if this can be done and also how you select containers)
    kubectl run butcher --image nginx 
    kubectl cp shop:/tmp/hello.txt buther:/tmp/hello.txt

    # lets copy a directory 
    kubectl run baker --image nginx 
    mkdir toolbox2 && cd toolbox2
    echo "hammer" > hammer.txt && echo "screw driver" > screw_driver.txt && echo "spanner" > spanner.txt
    cd ../

    # lets tar up toolbox2, use exec to untar it into a location and give it a new name
    tar cf - /toolbox2 | kubectl exec -i  baker -- tar xf - -C /toolbox3

    # lets to to the server and tar up the server side and send it to the pc and call it toolbox4
    kubectl exec baker -- tar cf - /toolbox3 | tar xf - -C /toolbox4

```

```YAML
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: shop
  name: shop
spec:
  containers:
  - image: redis
    name: shop-photos
    resources: {}
  - image: redis
    name: shop-front
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
