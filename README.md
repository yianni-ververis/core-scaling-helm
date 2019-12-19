# Helm Charts for Qlik Core Scaling OSS

Helm charts and values for Qlik Core Scaling
https://github.com/qlik-oss/core-scaling

### Prerequisites
- Kubernetes 1.12.5 or newer cluster with RBAC (Role-Based Access Control) enabled is required
- Helm 2.7.2 or newer or alternately the ability to modify RBAC rules is also required

### Create a cluster in Google Cloud
- Follow the instruction of the main repo, https://github.com/qlik-oss/core-scaling/blob/master/README.md#create-a-gke-cluster

### Create a cluster in Azure
- You can do it via the Azure portal as described here: https://community.qlik.com/t5/Qlik-Design-Blog/Azure-Kubernetes-Services-and-Qlik-Core/ba-p/1515128 or
- From the Azure CLI, by following these steps
1. Create the cluster, `az aks create -g my-resource-group -n name-of-my-cluster --location eastus --dns-name-prefix stage-aks --node-count 2 --node-vm-size Standard_DS2_v2s  --kubernetes-version 1.12.5`
1. Sync to the cluster, `az aks get-credentials -g my-resource-group -n name-of-my-cluster`

### Installation of Qlik Core Scaling
- **Helm** https://helm.sh/docs/using_helm/#installing-the-helm-client
- **Rbac** 
   - `kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=<yourProfile@qlik.com> --dry-run -o=yaml > create_role_binding.yml`
   - `kubectl apply -f create_role_binding.yml`
   - Add a ClusterRole for the Mira service, `kubectl apply -f ./rbac-config.yaml`
   - Add a secret with your license data, `kubectl create secret generic license-data --from-literal LICENSES_SERIAL_NBR=YOUR-LICENSE-SERIAL-NBR --from-literal LICENSES_CONTROL_NBR=YOUR-LICENSE-CONTROL-NBR`
- **Prometheus** `helm install --name prometheus ./charts/prometheus/ -f ./values/prometheus/dev.yaml`
- **Grafana** `helm install --name grafana ./charts/grafana`
- **Custom Metrics Api Server** `helm install custom-metrics-apiserver stable/prometheus-adapter -f ./values/custom-metrics-apiserver/dev.yaml`
- **License Service**, add your Control and Serial Number in ./charts/license-service/values.yaml and then run `helm install --name license-service ./charts/license-service`
- **Mira** `helm install --name mira ./charts/mira`
- **Qix Session** `helm install --name qix-session ./charts/qix-session`
- **Engine** `helm install --name engine ./charts/engine -f ./values/engine/values-dev.yaml`
- **NFS Aws** `helm install --name nfs ./charts/nfs -f ./values/nfs/values-aws.yaml`

### Modifications
- **Prometheus** `helm upgrade --install prometheus ./charts/prometheus -f ./values/prometheus/values-dev.yaml`
- **Grafana** `helm upgrade --install grafana ./charts/grafana`
- **Custom Metrics Api Server** `helm upgrade --install custom-metrics-apiserver ./charts/custom-metrics-apiserver`
- **License Service** `helm upgrade --install license-service ./charts/license-service`
- **Mira** `helm upgrade --install mira ./charts/mira`
- **Qix Session** `helm upgrade --install qix-session ./charts/qix-session`
- **Engine** `helm upgrade --install engine ./charts/engine`
- **NFS Aws** `helm upgrade --install nfs ./charts/nfs -f ./values/nfs/values-aws.yaml`

### Lint and check charts before installation
- **Prometheus** `helm install --dry-run --debug ./charts/prometheus`
- **Grafana** `helm install --dry-run --debug ./charts/grafana`
- **Custom Metrics Api Server** `helm install --dry-run --debug ./charts/custom-metrics-apiserver`
- **License Service** `helm install --dry-run --debug ./charts/license-service`
- **Mira** `helm install --dry-run --debug ./charts/mira`
- **Qix Session** `helm install --dry-run --debug ./charts/qix-session`
- **Engine** `helm install --dry-run --debug ./charts/engine`
- **NFS Aws** `helm install --dry-run --debug ./charts/nfs -f ./values/nfs/values-aws.yaml`

### Delete
- **Prometheus** `helm del --purge prometheus`
- **Grafana** `helm del --purge grafana`
- **Custom Metrics Api Server** `helm del --purge custom-metrics-apiserver`
- **License Service** `helm del --purge license-service`
- **Mira** `helm del --purge mira`
- **Qix Session** `helm del --purge qix-session`
- **Engine** `helm del --purge engine`
- **NFS Aws** `helm del --purge nfs`