**Step1**

Create an IAM policy which define the required permissions for AWS Load Balancer Controller.

**Step2:**  **Deploy ALB Controller:**

helm repo add eks https://aws.github.io/eks-charts

helm repo update eks

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \            
  -n kube-system \
  --set clusterName= ecommerce-cluster \
  --set serviceAccount.create=true \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set serviceAccount.annotations.eks\\.amazonaws\\.com/role-arn=<rolearn> \
  --set region= us-west-2 \
  --set vpcId=<your-vpc-id>

**Step3:**  **verify the deployment:**

kubectl get deployment -n kube-system aws-load-balancer-controller
