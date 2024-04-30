# Nginx K8s ingress controller

Helm installation Docs https://docs.nginx.com/nginx-ingress-controller/installation/installing-nic/installation-with-helm/

Requires MetalDb to be functional in order to install correctly. If not, the LoadBalancer service will hang getting an External-IP and the Helm install will fail.

