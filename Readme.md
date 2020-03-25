# Commands

kubectl get all
kubectl apply -f my-pods.yaml

kubectl describe pod <pod-name>

kubectl exec <pod-name> ls

kubectl -it exec <pod-name> sh









# Errors
- kubectl apply schema error
https://stackoverflow.com/questions/55417410/kubernetes-create-deployment-unexpected-schemaerror

- kubectl commands delays a lot like get all commands.
It might be a memory issue. so increase the minikube RAM memory on VM.
