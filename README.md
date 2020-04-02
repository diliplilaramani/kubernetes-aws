# AWS Setup - EC2 Instance - K8S

ssh -v -o ServerAliveInterval=60 -i "~/.ssh/PEM-FILE-NAME.pem" ec2-user@ec2-xx-xx-xx-xx.xx-xxxx-2.compute.amazonaws.com

# Steps


1. Setup instance on AWS - use Amazon AMI Free Tier
2. Install Kops (https://github.com/kubernetes/kops/blob/master/docs/install.md)
3. Install kubectl (https://github.com/kubernetes/kops/blob/master/docs/install.md#kubectl)
4. Follow K8S-AWS environment setup (https://github.com/kubernetes/kops/blob/master/docs/getting_started/aws.md)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. Setup IAM user - directly on Amazon or use command line<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Skip Configure DNS<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. Create cluster State storage<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4. Creating your first cluster<br />
5. For storage, setup StorageClass in storage-aws.yaml
6. Copy-paste and run kubectl apply -f storage-aws.yaml
7. Copy-paste and run kubectl apply -f mongo-stack.yaml
8. In services-aws.yaml file:<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. Remove nodePort and replace type: NodePort with LoadBalancer on webapp<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Remove nodePort and replace type: NodePort with ClusterIP on queue, api-gateway<br />
9. Run kubectl apply -f services-aws.yaml
10. Run kubectl apply -f workloads-aws.yaml
11. Check with kubectl get all

--------
## Extra stuff

### Whenever connect to instance then need to set below variables
export NAME=fleetman.k8s.local<br />
export KOPS_STATE_STORE=s3://kops2020-state-storage<br />

--------

# Delete the kubernetes Cluster
1. kops delete cluster --name ${NAME} --yes
2. Verify manually by visiting following pages - EC2, Volumes, Load Balancers, Auto-Scaling Group
3. Stop the main k8s instance manually from where you were managing k8s

--------

# Restart the kubernetes Cluster
1. Start the main k8s instance manually and click connect to get the ssh full url
2. SSH to instance
3. Run - history | grep export
4. !50 - line number for export NAME and KOPS_STATE_STORE
5. Press Ctlr+R to search commands - kops create cluster --zones us-east-2a ${NAME}
6. kops edit ig --name ${NAME} and change minSize=3 and maxSize=5
7. kops update cluster --name ${NAME} --yes
8. kops validate cluster
9. kubectl apply -f .
10. kubectl get all -o wide - To verify with  for node IP details
11. For webapp url - Go to Load Balancers and select one node with random string chars and copy the public dns
