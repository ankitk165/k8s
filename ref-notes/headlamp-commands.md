1. minikube addons enable headlamp

2. minikube service headlamp -n headlamp

3. export SECRET=$(kubectl get secrets --namespace headlamp -o custom-columns=":metadata.name" | grep "headlamp-token")
kubectl get secret $SECRET --namespace headlamp --template=\{\{.data.token\}\} | base64 --decode

or 

kubectl create token headlamp --duration 24h -n headlamp

4. minikube addons enable metrics-server

5. kubectl get pods -n headlamp

6. minikube addons disable 

Reference: https://minikube.sigs.k8s.io/docs/handbook/addons/headlamp/

