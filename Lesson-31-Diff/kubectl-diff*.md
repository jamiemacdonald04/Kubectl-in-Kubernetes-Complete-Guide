## diff

lets explore the diff command for comparing k8 objects.

``` shell
k run  test2 --image nginx --command  -- sh -c "echo 'jamie'" 
k run  test2 --image nginx -o yaml --dry-run=client  -- sh -c "echo 'jamie'" | kubectl diff -f -
```
