# kubectl set parent command

## setting up aliases

This is the parent for using the kubectl set

```shell
vim ~/.bashrc
```
The configurations I would add.
```shell
vim ~/.bashrc

export dry="--dry-run=client -o yaml"
alias k='kubectl'

set_minikube()
{
    kubectl config use-context minikube
}
alias kg="kubectl get "
alias kl="kubectl logs "
```
