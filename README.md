# Helm Charts for Qlik Core Scaling OSS

Helm charts and values for Qlik Core Scaling
https://github.com/qlik-oss/core-scaling

### Installation
- **Helm** https://helm.sh/docs/using_helm/#installing-the-helm-client
- **Prometheus** `helm install --name prometheus ./charts/prometheus/ -f ./values/prometheus/values-dev.yaml`
- **Grafana** `helm install --name grafana ./charts/grafana`
- **Custom Metrics Api Server** `helm install --name custom-metrics-apiserver ./charts/custom-metrics-apiserver`
- **License Service**, add your Control and Serial Number in ./charts/license-service/values.yaml and then run  `helm install --name license-service ./charts/license-service`
- **Mira** `helm install --name mira ./charts/mira`
- **Qix Session** `helm install --name qix-session ./charts/qix-session`

### Modifications
- if you make a change on Prometheus, run `helm upgrade --install prometheus ./charts/prometheus -f ./values/prometheus/values-dev.yaml`
- if you make a change on Grafana, run `helm upgrade --install grafana ./charts/grafana`
- if you make a change on Custom Metrics Api server, run `helm upgrade --install custom-metrics-apiserver ./charts/custom-metrics-apiserver`
- if you make a change on License Service, run `helm upgrade --install license-service ./charts/license-service`
- if you make a change on Mira, run `helm upgrade --install mira ./charts/mira`
- if you make a change on Mira, run `helm upgrade --install qix-session ./charts/qix-session`

### Lint and check charts before installation
- `helm install --dry-run --debug ./charts/prometheus`
- `helm install --dry-run --debug ./charts/grafana`
- `helm install --dry-run --debug ./charts/custom-metrics-apiserver`
- `helm install --dry-run --debug ./charts/license-service`
- `helm install --dry-run --debug ./charts/mira`
- `helm install --dry-run --debug ./charts/qix-session`

### Delete
- `helm del --purge prometheus`
- `helm del --purge grafana`
- `helm del --purge custom-metrics-apiserver`
- `helm del --purge license-service`
- `helm del --purge mira`
- `helm del --purge qix-session`