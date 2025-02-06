# kops-aws-cluster-setup

🔹 Prerequisites
Before running the script, ensure you have:

✅ An AWS account with permissions to create EC2, S3, and Route 53 resources
✅ A domain registered in Route 53 (e.g., myk8s.example.com)
✅ An S3 bucket for storing KOPS cluster state
✅ A t2.micro EC2 instance (for running the script) with:

Amazon Linux 2 / Ubuntu
IAM Role with Admin Access (or attach AdministratorAccess policy)

 Steps to Deploy
1️⃣ Create an EC2 instance with t2.micro and attach an IAM Role with Admin permissions
2️⃣ SSH into the instance:
ssh -i your-key.pem ubuntu@your-ec2-public-ip
3️⃣ Install required dependencies (if missing):
sudo apt update -y
sudo apt install -y awscli jq unzip
4️⃣ Clone this repository & navigate to it:
git clone https://github.com/your-username/kops-aws-cluster-setup.git
cd kops-aws-cluster-setup
5️⃣ Update the script variables in kops-cluster.sh

CLUSTER_NAME → Your domain (myk8s.example.com)
KOPS_STATE_STORE → Your S3 bucket
PARENT_DNS_ZONE → Your Route 53 Hosted Zone
NODE_COUNT & NODE_SIZE → Adjust based on workload
6️⃣ Make the script executable & run it:
chmod +x kops-cluster.sh
./kops-cluster.sh

✅ What This Script Does
✔ Creates a Kubernetes cluster on AWS using KOPS
✔ Configures Route 53 DNS for easy cluster access
✔ Deploys an Nginx application & exposes it via a LoadBalancer
✔ Configures AWS Security Groups to allow external traffic

🚀 Verifying the Cluster
📌 Check if the cluster is running:
kops validate cluster --state=s3://your-kops-state-bucket
📌 Check if nodes are running:
kubectl get nodes
📌 Check if LoadBalancer is working:
kubectl get svc
📌 Test Nginx in your browser:
http://<LoadBalancer-DNS>

