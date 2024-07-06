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

## Things I would like to improve

- I would like to stop using a nginx proxy server when the "Gateway" Should be able to handle it for me.
  - Problems here are...
    - Some things (unifi) expect to be spoken to https so HTTPRoutes don't work. [Cillium does not yet support TCPRoutes](https://docs.cilium.io/en/stable/network/servicemesh/gateway-api/gateway-api/) so I can't use the [method documented here.](https://gateway-api.sigs.k8s.io/guides/tls/#clientserver-and-tls)
    - Other things shared ports and NEED TCP/UDP routing (Adguard / DNS / mail)
    - Container registry. 'Could' be done but would required a secondary 'TLS termination' listener [with specific host config](https://gateway-api.sigs.k8s.io/guides/tls/#listeners-with-different-certificates) But this feels wrong to configure in place here when everything else is done in the container-registry folder.
- DNS is a forever problem which would be nice if I could find a solution for it... (maybe I manage public DNS in IaC then stop running a local DNS server?) (Is this possible with my provider)
  - This would allow me to remove hacks from [here](https://github.com/bl-robinson/terraform-k8s-libvirt-cluster/blob/master/configs/workers/cloud_init.cfg#L119) and [here](https://github.com/bl-robinson/terraform-k8s-libvirt-cluster/blob/master/configs/control_plane/cloud_init.cfg#L119)
  - Integrate adguard into this directly somehow?
- Applications missing...
  - Monitoring - This mostly works now... Would be good to have logging though! Pod logs stored for a couple of days would be helpful...
  - Immich - This really is going to demand a better persistent store solution... I have worked around the immediate requirement by tidying up my G-Cloud storage a bit.
  - Home Assistant? - Not really been used recently so can probably not worry about until I have a future need...
  - mailserver - I have a year of AWS free tier... so going to leave it there "for now" until I consider moving it back...
- Data server
  - This really should not be another VM. Invest in a proper fileserver at some point.