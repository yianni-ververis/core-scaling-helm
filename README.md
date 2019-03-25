# Helm Charts for Qlik Core Scaling OSS

Helm charts and values for Qlik Core Scaling
https://github.com/qlik-oss/core-scaling

### Installation
- Install Helm https://helm.sh/docs/using_helm/#installing-the-helm-client
- Install Prometheus `helm install --name prometheus ./charts/prometheus/ -f ./values/prometheus/values-dev.yaml`
- Install Grafana `helm install --name grafana ./charts/grafana/`
- Install Custom Metrics Api Server `helm install --name custom-metrics-apiserver ./charts/custom-metrics-apiserver/`

### Modifications
- if you make a change on Prometheus, run `helm upgrade --install prometheus ./charts/prometheus -f ./values/prometheus/values-dev.yaml`
- if you make a change on Grafana, run `helm upgrade --install grafana ./charts/grafana`

### Lint and check charts before installation
- `helm install --dry-run --debug ./charts/prometheus`
- `helm install --dry-run --debug ./charts/grafana`

### Delete
- `helm del --purge prometheus`
- `helm del --purge grafana`