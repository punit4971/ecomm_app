Create an Iam policy that allows the Cluster Autoscaler to modify your cluster's infrastructure.

Deploy the Cluster Autoscaler:

kubectl apply -f https://github.com/kubernetes/autoscaler/releases/download/cluster-autoscaler-1.23.0/cluster-autoscaler-autodiscover.yaml

After deploying, you must edit the deployment to specify your cluster's autoscaling groups.
(replace your node group name and cluster name)

Then, Annotate the deployment to prevent it from being evicted( to not shut it down ,if the server it’s on is running low on resources)

kubectl annotate deployment cluster-autoscaler \
  -n kube-system cluster-autoscaler.kubernetes.io/safe-to-evict="false"
