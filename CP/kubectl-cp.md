# kubectl cp

## Environment

We look into copying files from the computer to the server


```shell
    # set up and add another container, see the yaml below
    kubectl run shop --image redis -o yaml --dry-run=client > pod.yaml 
    # edit as below
    vim pod.yaml
    kubectl create -f pod.yaml
    kubectl exec shop  -- tar
  

    # copy a file from your computer to pods container
    echo "hello" > hello.txt
    kubectl cp ./hello.txt shop:/tmp/hello.txt -c shop-photos
    kubectl exec shop  -c shop-photos -- cat ./tmp/hello.txt


    # create a new file on the pod and copy it to this pc
    kubectl exec shop -c shop-front -it -- bash
    echo "goodbye" > goodbye.txt
    exit
    kubectl cp shop:goodbye.txt ./goodbye.txt -c shop-front 
    ls 

    # lets copy a directory 
    mkdir toolbox && cd toolbox
    echo "hammer" > hammer.txt && echo "screw driver" > screw_driver.txt && echo "spanner" > spanner.txt
    cd ../
    kubectl cp ./toolbox shop:/tmp/tooolbox  -c shop-photos --no-preserve=false
    kubectl exec shop  -c shop-photos -- ls ./tmp/tooolbox

    # from one pod to another (check if this can be done and also how you select containers)
    kubectl run butcher --image nginx 
    kubectl cp shop:/tmp/hello.txt butcher:/tmp/hello.txt
    # error: one of src or dest must be a local file specification and how would you specifiy the container

    # lets copy a directory kubec
    mkdir camara && cd camara
    echo "lens" > lens.txt && echo "film" > film.txt && echo "flash" > flash.txt
    cd ../

    # lets tar up camara, use exec to untar it into a location
    kubectl run camara-shop --image nginx 
    tar cf - camara | kubectl exec -i  camara-shop -- tar xf - -C ./
    kubectl exec camara-shop -- ls camara
   

    # lets to to the server and tar up the server side and send it to the pc and call it camara
    mkdir pod2pc
    kubectl exec camara-shop -- tar cf - camara | tar xf - -C ./pod2pc
    cd pod2pc/camara
    ls

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
  - image: nginx
    name: shop-photos
    resources: {}
  - image: redis
    name: shop-front
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
