# ecomm_app
Deploying Ecomm app using Kubernetes

**Deployment Process**

**1. Kubernetes Manifests**

Namespace: We created a dedicated namespace (ecommerce-app) to isolate the resources.

ConfigMap and Secrets: We stored non-sensitive data in a ConfigMap and sensitive data (like database passwords) in a Secret.

Persistent Volumes: Persistent storage was set up for MongoDB and RabbitMQ using PersistentVolume and PersistentVolumeClaim.

Deployments:

MongoDB was deployed as a StatefulSet to ensure stable network identities.


RabbitMQ and Backend were deployed as standard Deployments.

Frontend was also deployed as a Deployment.

Services:

We created services for each component (MongoDB, RabbitMQ, Backend, and Frontend) to allow them to communicate within the cluster.

Ingress: 

We used an Ingress resource to expose the frontend service externally, allowing users to access the application via a domain name.

**2. Cluster Autoscaling**

We can installed the Cluster Autoscaler to automatically adjust the number of nodes in the cluster based on resource demands using cluster-autoscaler.md

Configured Horizontal Pod Autoscaling (HPA) for the frontend & backend service to scale the number of pods based on CPU usage.

**3. Monitoring and Logging**

Prometheus and Grafana were deployed to monitor the performance and resource usage of the application.

We exposed Prometheus and Grafana using LoadBalancer service, They will be accessible on ExternalIP.

**For Debugging & Troubleshooting Scenarios added another debugging.md file.**




**How To deploy**

**Package your helm chart.**

helm package .


**Install the helm chart:**

helm install ecommerce-app ./ecommerce-app-0.1.0.tgz


**verify the delployment:**

helm status ecommerce-app

kubectl get all -n ecommerce-app
