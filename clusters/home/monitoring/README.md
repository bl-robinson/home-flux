# Monitoring Configuration

## Prometheus

- Configured using a single PersistentVolume as its backend store.
  - This is bound to my NFS for continuity of data.
- Internal Cluster Service for pod <-> pod comms
- HTTPRoute to bind access from rest of home network using standard ingress Gateway. (non-nginx)
- NodeExporter with configs to pull node level data.
  - Watch out for relabelings here to ensure we get the right labels at the end metrics
- Kube-State-Metrics for pod metrics
  - Again watch for relablings here. (so namespace becomes the 'Thing' namespace rather than 'exported_namespace)
- ServiceMonitors for
  - kubelet
  - K8s Api-Server

I have not spent a lot of time digging into and sanitizing the metrics gathered... I just lobbed a bunch of stuff together that'll probably give me what I need.

## Grafana

- HelmRelease from grafana themselves.
  - Inputs configured with some 3rd party dashboards "they look cool"
  - Datasource for internal prometheus cluster domain
  - Datasource for internal loki cluster domain (setup in logging)

