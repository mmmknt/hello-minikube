# 03_configuration

## prepair
`minikube start`

## apply
`kubectl apply -k .`

## get info
`kubectl get -k .`

## verify
`kubectl exec -it redis redis-cli`
`CONFIG GET maxmemory`
`CONFIG GET maxmemory-policy`

## delete pod
`kubectl delete pod redis`
