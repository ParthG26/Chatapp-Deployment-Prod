# ChatApp-Deployment-through-Kubernetes-and-Jenkins
ChatApp is deployed through Jenkins who will pull code from Github repository and use the Dockerfile to build and image which will then be pushed into ECR and the K8s cluster will take the image from ECR and deploy a pod from it
