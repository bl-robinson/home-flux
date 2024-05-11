# Unifi Controller

This is built out using https://github.com/linuxserver/docker-unifi-network-application

Host CPU passthrough defined in https://github.com/bl-robinson/terraform-k8s-libvirt-cluster/blob/e931ab57b8894d76e5500f4aae832ac3522d0041/worker.tf#L49 is required for mongodb > v4.

Beware of state things.

The environment variables set on both Unifi and Mongo to handle their connectivity are only set on initial setup.

They do not get reset if you update/change them. So a change to "MONGO_PASS" for instance will do nothing.

## Cut over from other hosted.

To Cut over from self hosted unifi to this k8s one is pretty simple.

- Take a backup from the unifi controller we are coming from.
- When setting this instance up restore from the backup. (This will take a long time)
- In the old controller ensure under "device authentication" ssh is enabled and take a note of the password.
- SSH to each unifi device individually and run `set-inform http://10.0.0.104:8080/inform` to encorage the device to move to the new controller.
- Once all devices are 'ready' in the new controller turn off the old one.
