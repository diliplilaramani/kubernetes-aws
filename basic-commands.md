# Kubernetes - Quick Command Reference


## Minikube

### minikube start
Starts minikube. If this hangs then see error #2 end of this page.

### minikube stop
Stops the minikube virtual machine.

### minikube delete
Do this to completely delete the minikube image. Delete if minikube is refusing to start or failing randomly.

### minikube env
Find out the required environment variables to connect to the docker daemon running in minikube.

### minikube ip
Find out the ip address of minikube. Needed for browser access.

## Kubectl basic commands

### kubectl get all
List all objects that you’ve created. Pods at first, later,
ReplicaSets, Deployments and Services

### kubectl get pods -o wide
List all pods with their IP and Node details

### kubectl apply –f <yaml file>
Either creates or updates resources depending on the contents of the yaml file

### kubectl apply –f .
Apply all yaml files found in the current directory

### kubectl describe pod <name of pod>
Gives full information about the specified pod

### kubectl exec –it <pod name> <command>
Execute the specified command in the pod’s container.
Doesn’t work well in Cygwin.

### kubectl get (pod | po | service | svc | rs | replicaset | deployment | deploy)
Get all pods or services. Later in the course, replicasets and deployments.

### kubectl get po --show-labels
Get all pods and their labels

### kubectl get po --show-labels -l {name}={value}
Get all pods matching the specified name:value pair

### kubectl delete po <pod name>
Delete the named pod. Can also delete svc, rs, deploy

### kubectl delete po --all
Delete all pods (also svc, rs, deploy) Deployment Management

### kubectl rollout status deploy <name of deployment>
Get the status of the named deployment

### kubectl rollout history deploy <name of deployment>
Get the previous versions of the deployment

### kubectl rollout undo deploy <name of deployment>
Go back one version in the deployment. Also optionally -- to-revision=<revision number>


# Errors
### 1. kubectl apply schema error
https://stackoverflow.com/questions/55417410/kubernetes-create-deployment-unexpected-schemaerror

### 2. minikube or kubectl commands delays a lot.
It might be a memory issue. so increase the minikube RAM memory on VM.
