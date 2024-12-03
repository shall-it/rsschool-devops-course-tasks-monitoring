# rsschool-devops-course-tasks-monitoring


## Task 7
https://github.com/rolling-scopes-school/tasks/blob/master/devops/modules/4_monitoring-configuration/task_7.md

### To deploy Prometheus locally
1. Add Bitnami Helm repository:
`helm repo add bitnami https://charts.bitnami.com/bitnami`
2. Update Helm repositories:
`helm repo update`
3. Create a namespace for Prometheus:
`kubectl apply -f prometheus/prometheus-namespace.yaml`
4. Install Prometheus using Helm and prometheus-values.yaml file from current repository:
`helm install prometheus bitnami/prometheus --namespace monitoring -f prometheus/prometheus-values.yaml`
5. Install Node Exporter (for node-level metrics):
`helm install node-exporter bitnami/node-exporter --namespace monitoring`
6. Install Kube State Metrics (for Kubernetes object metrics):
`helm install kube-state-metrics bitnami/kube-state-metrics --namespace monitoring`

All these steps are automated with GitHub Actions and allow you to deploy Prometheus and additional tools to K8s cluster by Helm with execution of all required steps before.
Important notice! Please do not forget to setup GHA credentials which used as environment variables.

### To deploy Grafana locally
1. Add Bitnami Helm repository:
`helm repo add bitnami https://charts.bitnami.com/bitnami`
2. Update Helm repositories:
`helm repo update`
3. Create a namespace for Grafana:
`kubectl apply -f grafana/grafana-namespace.yaml`
4. Create configmap with respective dashboard json-file for Grafana:
`kubectl create configmap k8s-dashboard --from-file=grafana/1860_rev37.json -n monitoring`
5. Install Grafana using Helm and grafana-values.yaml file from current repository:
`helm upgrade --install grafana bitnami/grafana --namespace monitoring -f grafana/grafana-values.yaml`
