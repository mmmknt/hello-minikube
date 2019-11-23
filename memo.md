# cheat paper
## minikube
### start minikube and create cluster
`minikube start`
### get the url of exposed service
`minikube service hello-minikube --url`
### stop minikube and cluster
`minikube stop`
### delete local cluster
`minikube delete`

## Kubernetes
### create deployment
`kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10`
### expose service
`kubectl expose deployment hello-minikube --type=NodePort --port=8080`
### delete service
`kubectl delete services hello-minikube`
### delete deployment
`kubectl delete deployment hello-minikube`

# read later
https://kubernetes.io/docs/setup/