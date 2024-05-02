# Web Ingress

This is the main ingress LB which is used to receive port forwarded traffic from the router.

Individual applications should have their HTTPRoute configured with themselves not here.

This can probably be replaced by just 'config' on Gateways. But for now as its a migration. 