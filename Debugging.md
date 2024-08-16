**Debugging & Troubleshooting Scenarios**


**Frontend Accessibility:**


Issue: The frontend service isn't accessible from outside after deployment.


Task: Check the networking setup and Ingress configuration to make sure the frontend can be reached.


Commands to run:


kubectl get services -n <namespace> to see if the service type is LoadBalancer or Ingress.


kubectl get ingress -n <namespace> to check if Ingress is set up correctly.


kubectl describe ingress <ingress-name> -n <namespace> to get details on the Ingress rules.


kubectl logs <ingress-controller-pod> -n <ingress-namespace> to check Ingress controller logs for issues.



**Intermittent Backend-Database Connectivity:**


Issue: The backend sometimes loses connection to MongoDB, causing errors.


Task: Look into potential issues like network policies, service discovery problems, or MongoDB settings.


Commands to run:

kubectl logs <mongodb-pod> -n <namespace> to check MongoDB logs for errors.

kubectl get networkpolicy -n <namespace> to see if any network policies are blocking traffic.

kubectl exec -it <backend-pod> -n <namespace> -- curl <mongodb-service>:<port> to test connectivity from the backend to MongoDB.

kubectl top pods -n <namespace> to check if there are any resource constraints affecting connectivity.


**Order Processing Delays:**


Issue: Users are experiencing delays with order processing, possibly due to RabbitMQ.


Task: Investigate the RabbitMQ setup and tweak it to speed up message processing.


Commands to run:


kubectl port-forward <rabbitmq-pod> 15672:15672 -n <namespace> to access the RabbitMQ management UI and check queue status.

kubectl logs <rabbitmq-pod> -n <namespace> to inspect RabbitMQ logs for any issues.

kubectl top pods -n <namespace> to ensure consumers (backend) have enough resources.

kubectl get hpa -n <namespace> to check if Horizontal Pod Autoscaling is properly configured for the backend service.
