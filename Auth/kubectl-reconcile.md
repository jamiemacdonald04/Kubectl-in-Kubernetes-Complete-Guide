# kubectl reconcile

Reconciles rules for RBAC role, role binding, cluster role, and cluster role binding objects. 
This is prefered over merge because of the extra rules on merging that are provided.

## Command

Arguments we are using.

```shell
  # lets create a role 
  kubectl create role france --verb=get --verb=list --verb=watch --resource=pods --resource=deployments
  kubectl create rolebinding french-binding --role=france --user=user1 --user=user2 --serviceaccount=default:default

  kubectl describe role france
  kubectl create role france --verb=get --verb=watch --resource=pods --dry-run=client -n default -o yaml > role.yaml
  kubectl auth reconcile -f role.yaml
  kubectl describe role france
  kubectl auth reconcile -f role.yaml --remove-extra-permissions
  kubectl describe role france

  kubectl describe rolebinding french-binding
  kubectl create rolebinding french-binding --role=france --user=user3 --serviceaccount=default:default -n default  --dry-run=client -o yaml > rolebinding.yaml
  kubectl auth reconcile -f rolebinding.yaml
  kubectl describe rolebinding french-binding
  kubectl auth reconcile -f rolebinding.yaml --remove-extra-subjects  --dry-run=client
  kubectl auth reconcile -f rolebinding.yaml --remove-extra-subjects 
  kubectl describe rolebinding french-binding

```
