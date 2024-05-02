# Cert-manager Installation

This is to install [cert-manager](https://cert-manager.io/) to handle letsencrypt certificate generation/renewal.

Requires the web-ingress Kustomization. As this is used as a central entrypoint for PortForwarded traffic.

Certificates should be created in the namespace / application they belong with. NOT in this folder.
The operator handles auto-creation of specific routes on the Gateway.