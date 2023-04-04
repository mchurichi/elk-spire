## ELK-SPIRE demo deployment

### Overview

The following Kubernetes manifests setup a complete SPIRE + ELK + Telemetry deployment:
- SPIRE
    - SPIRE Server Statefulset
    - SPIRE Agent DaemonSet
    - SPIRE Controller Manager
- ELK stack
    - A central Elasticsearch instance
    - A Logstash agent next to each SPIRE Server and Agent
    - A Kibana instance
- Telemetry
    - A Prometheus instance
    - A StatsD + Graphite instance

Each SPIRE Server and Agent have enabled DEBUG level logging to a file on disk. The Logstash agents collect these logs and sends them to Elasticsearch.

All SPIRE components are also configured to send metrics to both Prometheus and StatsD.

### Setup

- Copy `spire/logstash.sample-env` to `spire/logstash.env`
- Fill the variables with logstash credentials
- Apply the kustomize manifests in the root directory: `kubectl -k .`