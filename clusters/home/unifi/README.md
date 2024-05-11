# Unifi Controller

This is built out using https://github.com/linuxserver/docker-unifi-network-application

Host CPU passthrough defined in https://github.com/bl-robinson/terraform-k8s-libvirt-cluster/blob/e931ab57b8894d76e5500f4aae832ac3522d0041/worker.tf#L49 is required for mongodb > v4.

Beware of state things.

The environment variables set on both Unifi and Mongo to handle their connectivity are only set on initial setup.

They do not get reset if you update/change them. So a change to "MONGO_PASS" for instance will do nothing.
