# Example: Deploying PHP Guestbook application with Redis

## prepair
`minikube start`

## Start up the Redis Master
### Creating the Redis Master Deployment
`kubectl apply -f application/guestbook/redis-master-deployment.yaml`
`kubectl get pods`
`kubectl logs -f <POD_NAME>`

### Creating the Redis Master Service
`kubectl apply -f application/guestbook/redis-master-service.yaml`
`kubectl get service`

## Start up the Redis Server
### Creating the Redis Slave Deployment
`kubectl apply -f application/guestbook/redis-slave-deployment.yaml`
`kubectl get pods`

### Creating the Redis Slave Service
`kubectl apply -f application/guestbook/redis-slave-service.yaml`
`kubectl get services`

## Set up and Expose the Guestbook Frontend
### Creating the Guestbook Frontend Deployment
`kubectl apply -f application/guestbook/frontend-deployment.yaml`
`kubectl get pods -l app=guestbook -l tier=frontend`

### Creating the Frontend Service
`kubectl apply -f application/guestbook/frontend-service.yaml`
`kubectl get services`

### Viewing the Frontend Service via NodePort
`minikube service frontend --url`

## Scale the Web Frontend
`kubectl scale deployment frontend --replicas=5`
`kubectl get pods`
`kubectl scale deployment frontend --replicas=2`
`kubectl get pods`

## Cleaning up
`kubectl delete deployment -l app=redis`
`kubectl delete service -l app=redis`
`kubectl delete deployment -l app=guestbook`
`kubectl delete service -l app=guestbook`
`kubectl get pods`
`minikube stop`
`minikube delete`