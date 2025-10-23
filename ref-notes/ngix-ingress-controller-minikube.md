1. minikube addons enable ingress
2. kubectl get pods -n ingress-nginx
3. kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
4. kubectl get deployment web 
5. kubectl expose deployment web --type=NodePort --port=8080
6. kubectl get service web
7. minikube service web --url # The command must be run in a separate terminal.
8. curl http://127.0.0.1:62445 | output from previous
9. kubectl apply -f https://k8s.io/examples/service/networking/example-ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  ingressClassName: nginx
  rules:
    - host: hello-world.example
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: web
                port:
                  number: 8080
 
 10. kubectl get ingress

 11. minikube tunnel # separate window
 12. curl --resolve "hello-world.example:80:127.0.0.1" -i http://hello-world.example
 13. kubectl create deployment web2 --image=gcr.io/google-samples/hello-app:2.0
 14. kubectl get deployment web2 
 15. kubectl expose deployment web2 --port=8080 --type=NodePort
 16. kubectl apply -f example-ingress.yaml
 
  - path: /v2
  pathType: Prefix
  backend:
    service:
      name: web2
      port:
        number: 8080

17. minikube tunnel

curl --resolve "hello-world.example:80:127.0.0.1" -i http://hello-world.example
curl --resolve "hello-world.example:80:127.0.0.1" -i http://hello-world.example/v2

Refrence: https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/