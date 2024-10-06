# kubectl set parent command

## setting up aliases

Setting up aliases in the bashrc file is a good way to save time and make your life easier.
I would say this is especially true when sitting the ckad exam.

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
