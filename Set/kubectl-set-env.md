# kubectl set 

## Setting Environment

Lets explore how to set enviroment vars

```shell
# environments
  # Update deployment 'summer' with a new environment variable
  kubectl create deploy summer --image nginx
  kubectl set env deployment summer weather=sunny
  
  # list out environment vars 
  kubectl set env deployment summer --list
  kubectl set env pods --all --list
  
  # create a pod and update it to have env with a key value pair
  kubectl create deploy winter --image nginx | kubectl set env deploy winter weather=snow
  
  # Update all containers in all deployments in the project to have ENV=prod
  kubectl set env deploy --all ENV=prod

  # remove that environment variable
  kubectl set env deploy --all ENV=prod
  
  # Import environment from a secret with a prefix
  kubectl create secret generic secret-sun-day --from-literal=december=sun
  kubectl set env --from=secret/secret-sun-day deploy winter  --prefix=VAR_ 
  kubectl set env deployment winter --list
  
  # Import environment from a config map
  kubectl create configmap bank-holiday --from-literal=May=Rain --from-literal=October=Sun
  kubectl set env --from=configmap/bank-holiday deployment/summer
   kubectl set env deployment summer --list
  
  # Import specific keys from a config map (same proccess for a secret)
  kubectl create deployment month-october --image nginx 
  kubectl set env --keys=October --from=configmap/bank-holiday deployment month-october
  kubectl set env deployment month-october --list
  
  # Set some of the local shell environment into a deployment config on the server
  kubectl create deploy spring --image nginx
  export WEATHER=RUBBISH 
  echo WEATHER=$WEATHER | kubectl set env -e - deployment spring
  kubectl set env deployment spring --list
```
