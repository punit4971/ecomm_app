Install Prometheus and Grafana via Helm:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

Then Deploy prometheus Operator,
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace

Now, expose Prometheus and Grafana using a LoadBalancer service in Kubernetes. you can access them via externalIP. 
You can also use DNS and managed SSL certificates to provide a secure and user-friendly URL.