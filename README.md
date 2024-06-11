# Home-Flux

This repository should be configured as a Target for [fluxcd](https://fluxcd.io/)

The basic elements are

1. A GitRepository pointing at this
2. A Kustomization pointing at the cluster root folder. (It will read the kustomization.yaml and then follow resources from there. )

Example required to get it applied.

```
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: home-flux
spec:
  interval: 5m0s
  ref:
    branch: master
  url: https://github.com/bl-robinson/home-flux.git
  secretRef:
    name: git-token
---
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: home-flux
  namespace: flux-system
spec:
  interval: 10m
  sourceRef:
    kind: GitRepository
    name: home-flux
  path: "./clusters/home/"
  prune: true
  timeout: 1m

```

I have actively chosen to split independent 'Applications' into their own Kustomizations to allow...
1. One being broken will not block others
2. I can easily remove/add sections of this repo by just commenting them out in the root kustomization.yaml
