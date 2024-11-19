1. Install helm
2. Helm --version
3. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
4. helm repo update  For Set Up
5. helm install prometheus prometheus-community/prometheus --namespace monitoring --create-namespace
6. kubectl get pods -n monitoring verify installetion
7. kubectl port-forward -n monitoring svc/prometheus-server 9090:80 (Optional)
   Set Up Grafana with Helm
8. helm repo add grafana https://grafana.github.io/helm-charts
9. helm repo update
10. helm install grafana grafana/grafana --namespace monitoring
