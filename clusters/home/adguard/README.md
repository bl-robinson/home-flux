# Adguard

This is simply a deployment of [Adguard home](https://github.com/AdguardTeam/AdGuardHome#getting-started) which I use to help with ad blocking at DNS.

It is configured to use my K8s hosted DNS as its primary upstream, with 8.8.8.8 as a fallback.

The rest of my network is set to use this LoadBalancer endpoint as its DNS server.

## Notes

- I'd like to look at getting the config for this into a ConfigMap
- I need to deal with the plain text password that would be stored in it though.
- For now I have just persisted all config into the NFS VolumeMounts configured in the Deployment.

