# Web Ingress

There is a 'Main' Gateway using the new K8s Gateway API. That is used for non-web facing things. (Internal network only)
  - Applications accessed via this have their HTTPRoute configured with themselves (in their own namespaces) not here.
  - Although the certificated used by it is setup and connected here.
  - This Gateway terminates SSL at the gateway.

There is a second Gateway which does SSL Passthrough to a deployment of the [docker-web](https://github.com/bl-robinson/docker-web) container repo.

- This is the Web-Facing endpoint which I expose via port-forward.
- This is done mostly because some apps need to be spoken to on SSL but [Cillium does not yet support TCPRoutes](https://docs.cilium.io/en/stable/network/servicemesh/gateway-api/gateway-api/) so I can't use the [method documented here.](https://gateway-api.sigs.k8s.io/guides/tls/#clientserver-and-tls)
- Note: Cert manager uses the port 80 endpoint of this for certificate validation, (It adds is own HTTPRoutes to connect to this. )
