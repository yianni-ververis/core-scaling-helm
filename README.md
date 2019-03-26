# Helm Charts for Qlik Core Scaling OSS

Helm charts and values for Qlik Core Scaling
https://github.com/qlik-oss/core-scaling

### Installation
- **Helm** https://helm.sh/docs/using_helm/#installing-the-helm-client
- **Rbac** 
 - `kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=<yourProfile@qlik.com> --dry-run -o=yaml > create_role_binding.yml`
 - `kubectl apply -f create_role_binding.yml`
 - `kubectl apply -f ./rbac-config.yaml`
- **Prometheus** `helm install --name prometheus ./charts/prometheus/ -f ./values/prometheus/values-dev.yaml`
- **Grafana** `helm install --name grafana ./charts/grafana`
- **Custom Metrics Api Server** `helm install --name custom-metrics-apiserver ./charts/custom-metrics-apiserver`
- **License Service**, add your Control and Serial Number in ./charts/license-service/values.yaml and then run `helm install --name license-service ./charts/license-service`
- **Mira** `helm install --name mira ./charts/mira`
- **Qix Session** `helm install --name qix-session ./charts/qix-session`
- **Engine** `helm install --name engine ./charts/engine -f ./values/engine/values-dev.yaml`

### Modifications
- **Prometheus** `helm upgrade --install prometheus ./charts/prometheus -f ./values/prometheus/values-dev.yaml`
- **Grafana** `helm upgrade --install grafana ./charts/grafana`
- **Custom Metrics Api Server** `helm upgrade --install custom-metrics-apiserver ./charts/custom-metrics-apiserver`
- **License Service** `helm upgrade --install license-service ./charts/license-service`
- **Mira** `helm upgrade --install mira ./charts/mira`
- **Qix Session** `helm upgrade --install qix-session ./charts/qix-session`
- **Engine** `helm upgrade --install engine ./charts/engine`

### Lint and check charts before installation
- **Prometheus** `helm install --dry-run --debug ./charts/prometheus`
- **Grafana** `helm install --dry-run --debug ./charts/grafana`
- **Custom Metrics Api Server** `helm install --dry-run --debug ./charts/custom-metrics-apiserver`
- **License Service** `helm install --dry-run --debug ./charts/license-service`
- **Mira** `helm install --dry-run --debug ./charts/mira`
- **Qix Session** `helm install --dry-run --debug ./charts/qix-session`
- **Engine** `helm install --dry-run --debug ./charts/engine`

### Delete
- **Prometheus** `helm del --purge prometheus`
- **Grafana** `helm del --purge grafana`
- **Custom Metrics Api Server** `helm del --purge custom-metrics-apiserver`
- **License Service** `helm del --purge license-service`
- **Mira** `helm del --purge mira`
- **Qix Session** `helm del --purge qix-session`
- **Engine** `helm del --purge engine`