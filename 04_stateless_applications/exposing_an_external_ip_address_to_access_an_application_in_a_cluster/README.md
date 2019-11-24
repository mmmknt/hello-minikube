# exposing an external ip address to access an application in a cluster
https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/

## prepair
`gcloud container clusters create expose-external-ip-address`
`gcloud container clusters get-credentials expose-external-ip-address`

## apply
`kubectl apply -f load-balancer-example.yaml`

## display Deployment information
`kubectl get deployments hello-world`
`kubectl describe deployments hello-world`

## display ReplicaSet objects information
`kubectl get replicasets`
`kubectl describe replicasets`

## create a service object that expose the deployment
`kubectl expose deployment hello-world --type=LoadBalancer --name=my-service`

## display Service information
`kubectl get services my-service`
`kubectl describe services my-service`

## display pod information with IP
`kubectl get pods --output=wide`

## access application
`curl http://<external-ip>:<port>`

## delete service
`kubectl delete services my-service`

## delete deployment
`kubectl delete deployment hello-world`

## delete cluster
`gcloud container clusters delete expose-external-ip-address`