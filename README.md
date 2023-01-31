# OKD-Mastodon-Metrics
A simple approach to grab metrics from Mastodon running via Helm Chart in OKD

The basic setup idea come from this wonderfull post and all credits regarding grafana dashboard and metrics mapping goes to IPng Networks GmbH / The author of the blogpost.

https://ipng.ch/s/articles/2022/11/27/mastodon-3.html

Based on the wonderful statsd exporter:
https://github.com/prometheus/statsd_exporter

This should work on OKD/Openshift and on clusters where the Prometheus Operator is installed and watches the needed namespaces.

Installation steps:
- If using Openshift or OKD make sure that User Workload Monitoring is activated
- adjust values of the mastodon helm chart:
  ```
  metrics:
    statsd:
      # -- Enable statsd publishing via STATSD_ADDR environment variable
      # -- address consists of <servicename>.<namespace>.svc.cluster.local:9125
      address: "statsd-exporter.mastodon.svc.cluster.local:9125"
  ```
- clone the repository and adjust namespace value inside kustomization to your mastodon namespace.
- apply with oc apply -k .
