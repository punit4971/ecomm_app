
Create Iam role for EKS & attach following policies to the role:
* AmazonEKSClusterPolicy
* AmazonEKSServicePolicy

Create EKS Cluster using Console or CLI:
aws eks create-cluster \
  --name ecommerce-cluster \
  --region us-west-2 \
  --kubernetes-version 1.27 \
  --role-arn arn:aws:iam::<account-id>:role/<eks-role> \
  --resources-vpc-config subnetIds=<subnet-ids>,securityGroupIds=<security-group-ids>

Create a Node group:
aws eks create-nodegroup \
  --cluster-name ecommerce-cluster \
  --nodegroup-name ecommerce-nodes \
  --scaling-config minSize=2,maxSize=4,desiredSize=3 \
  --disk-size 20 \
  --subnets <subnet-ids> \
  --instance-types t3.medium \
  --ami-type AL2_x86_64 \
  --node-role arn:aws:iam::<account-id>:role/<node-instance-role> \
  --region us-west-2

Update Your Kubeconfig:
aws eks update-kubeconfig --name ecommerce-cluster --region us-west-2

Verify nodes:
kubectl get nodes

Then, Deploy your application.
