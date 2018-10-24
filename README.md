# Hello Kubernetes -  Topics
* How to deploy a docker to kubernetes
* How to deploy from yaml file ( service & deployment )
* ConfigMap & Secret: Best practices
* Nginx Ingress ( In progress ...)

The default "Hello world!" message displayed can be overridden using the `MESSAGE` environment variable.

The default port of 8080 can be overriden using the `PORT` environment variable.

# Deploy

All deployment with K8s is located in yaml directory.

You can deploy the image to your Kubernetes cluster one of two ways:

Deploy using the hello-kubernetes.yaml, which contains definitions for the service and deployment objects:

```
$ cd docker-hello/ && docker build -t gcr.io/${PROJECT_ID}/hello-app:v1.6 .
$ gcloud docker -- push gcr.io/${PROJECT_ID}/hello-app:v1.6
$ kubectl apply -f yaml/hello-app.yaml
```

Or, deploy by executing the following `run` and `expose` commands on `kubectl`. 

```bash
$ kubectl run hello-app --replicas=3 --image=gcr.io/hello-app:v1.0 --port=8080
$ kubectl expose deployment hello-app --type=LoadBalancer --port=80 --target-port=8080 --name=hello-app
```

This will display a **Hello world!** message when you hit the service endpoint in a browser. You can get the service endpoint ip address by executing the following command and grabbing the returned external ip address value:

```bash
$ kubectl get svc
```

# Creating the ConfigMap and Secret from file
```
kubectl create secret generic env-secret --from-env-file=./secret/secret.env
kubectl create configmap env-config --from-env-file=./config/config.env

kubectl get secret
kubectl get configmap
```

# Replace/Update the ConfigMap and Secret
```
kubectl create configmap env-config --from-env-file=./config/config.env -o yaml --dry-run | kubectl replace -f -
kubectl create secret generic env-secret --from-env-file=./secret/secret.env -o yaml --dry-run | kubectl replace -f -
```

# How to update image for a deployment
```
kubectl get svc
Update image version in yaml/hello-app.yaml then kubectl apply -f yaml/hello-app.yaml or
kubectl apply -f yaml/hello-app.yaml --force=true
kubectl rollout status deployment/hello-app
```
# Print deployment details
```
kubectl describe deployment
```
# Print env pods
```
kubectl get pods
kubectl exec -ti hello-app-8568d9f9df-khdv2 env
```
