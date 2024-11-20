# Cluster logging config

This works now and is integrated as a datasource in [grafana](../../clusters/home/monitoring/grafana.yaml)

This makes use of 2 things...

1. The [logging operator](https://kube-logging.dev/4.0/)
    - This is configured using fluent bit and fluendt.
    - With a single ClusterFlow and ClusterOutput pointing at the Loki
    - Watch out for setting the control-namespace in the Helm chart, without this the ClusterFlow and ClusterOutput are not actioned correctly.
2. [Grafana loki](https://grafana.com/docs/loki/latest/)
    - Datasource for this configured in the monitoring namespace with grafana.
    - Setup using a 'pre-created' PersistentVolume. (To allow me to create one using NFS)
    - Configured in single binary mode, with only one replica to avoid issues with multiple PersistentVolumes being needed.
