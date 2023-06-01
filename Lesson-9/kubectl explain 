# Explain

## Environment

No environment setup required.

## Explain and grep

Let's use the explian kubectl command to get clues how to format our yaml.

``` shell
k explain pod 
k explain pods.spec
k explain pods.spec.volumes.secret
k explain pods.spec.volumes.secret --recursive

k explain pod --recursive | grep -iA20 -B20 envfrom

```