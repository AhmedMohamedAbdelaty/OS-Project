# Deploying a Web App on Kubernetes

This quick tutorial walks through deploying a docker image on Kubernetes and accessing the running app.

## Prerequisites

- Kubernetes cluster
- Docker image pushed to Docker Hub

## Create Deployment

We will deploy the docker image `<your-docker-id>/web-app` using a Kubernetes Deployment.

Here is the deployment manifest `deploy.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
        - name: web-app
          image: <your-docker-id>/web-app
          ports:
            - containerPort: 80
```

Apply the deployment:

```bash
kubectl apply -f deploy.yaml
```

This will create 3 replicas of the web app container.

## Access the App

To access the app from outside the cluster, we can create a port-forward:

```bash
kubectl port-forward deployment/web-app-deployment 8080:80
```

Now the app will be available on localhost:8080.

This quick tutorial showed how to deploy a dockerized web app on Kubernetes and access it with port-forwarding.
