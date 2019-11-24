# Learn Kubernetes Basics
https://kubernetes.io/docs/tutorials/kubernetes-basics/

# Module 1 Create a Cluster
## step1: Cluster up and running
`minikube version`
`minikube start`
## step2: Cluster version
`kubectl version`
## step3: Cluster details
`kubectl cluster-info`
`kubectl get nodes`

# Module 2 Deploy an App
## step1: kubectl basics
`kubectl version`
`kubectl get nodes`
## step2: Deploy our app
`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`
`kubectl get deployments`
## step3: View our app
```
echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n";
kubectl proxy
```
`curl http://localhost:8001/version`
```
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME
```

# Module 3 Explore Your App
## step1: Check application configuration
`kubectl get pods`
`kubectl describe pods`
## step2: Show the app in the terminal
`echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy`
```
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME
```
`curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/`
## step3: View the container logs
`kubectl logs $POD_NAME`
## step4: Executing command on the container
`kubectl exec $POD_NAME env`
`kubectl exec -ti $POD_NAME bash`
`cat server.js`
`curl localhost:8080`
`exit`

# Module 4 Expose Your App Publicly
## step1: Create a new service
`kubectl get pods`
`kubectl get services`
`kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080`
`kubectl get services`
`kubectl describe services/kubernetes-bootcamp`
```export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
echo NODE_PORT=$NODE_PORT
```
`curl $(minikube ip):$NODE_PORT`
## step2: Using labels
`kubectl describe deployment`
`kubectl get pods -l run=kubernetes-bootcamp`
`kubectl get services -l run=kubernetes-bootcamp`
```
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME
```
`kubectl label pod $POD_NAME app=v1`
`kubectl describe pods $POD_NAME`
`kubectl get pods -l app=v1`
## step3: Deleting a service
`kubectl delete service -l run=kubernetes-bootcamp`
`kubectl get services`
`curl $(minikube ip):$NODE_PORT`
`kubectl exec -ti $POD_NAME curl localhost:8080`

# Module 5 Scale Your App
## step1: Scaling a deployment
`kubectl get deployments`
`kubectl scale deployments/kubernetes-bootcamp --replicas=4`
`kubectl get deployments`
`kubectl get pods -o wide`
`kubectl describe deployments/kubernetes-bootcamp`
## step2: Load Balancing
`kubectl describe services/kubernetes-bootcamp`
```
export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
echo NODE_PORT=$NODE_PORT
```
`curl $(minikube ip):$NODE_PORT`
## step3: Scale Down
`kubectl scale deployments/kubernetes-bootcamp --replicas=2`
`kubectl get deployments`
`kubectl get pods -o wide`

# Module 6 Update your app
## step 1: Update the version of the app
`kubectl get deployments`
`kubectl get pods`
`kubectl describe pods`
`kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2`
`kubectl get pods`

## step 2: Verify an update
`kubectl describe services/kubernetes-bootcamp`
```
export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
echo NODE_PORT=$NODE_PORT
```
`curl $(minikube ip):$NODE_PORT`
`kubectl rollout status deployments/kubernetes-bootcamp`
`kubectl describe pods`

## step 3: Rollback an update
`kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10`
`kubectl get deployments`
`kubectl get pods`
`kubectl rollout undo deployments/kubernetes-bootcamp`
`kubectl get pods`
`kubectl describe pods`