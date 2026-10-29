# Experiment 9: Automate a Containerized Application Using Kubernetes

## Aim
To automate the deployment and management of the containerized application developed in Experiment 7 using Kubernetes.

## Objectives
1. To understand Kubernetes container orchestration.
2. To deploy a Dockerized web application using Kubernetes.
3. To automate application deployment using Kubernetes configuration files.
4. To manage pods and deployments.
5. To expose the application using a Kubernetes Service.

## Software Requirements
- Docker
- Kubernetes
- kubectl
- Minikube or another Kubernetes cluster
- Web browser
- Application source code from Experiment 7

## Introduction
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It uses Deployments to maintain the desired number of application replicas and Services to provide network access to applications.

## Procedure
1. Install Docker and configure a Kubernetes cluster.
2. Verify that the cluster is running.
3. Build the Docker image for the application from Experiment 7.
4. Make the image available to the Kubernetes cluster or publish it to a container registry.
5. Create a Kubernetes Deployment configuration.
6. Apply the configuration using kubectl.
7. Verify the running pods and Deployment status.
8. Create a Service to expose the application.
9. Access the application and verify its output.

## Kubernetes Deployment Configuration

Save the following as `deployment.yaml`. This example uses the Nginx image; replace it with the image for your Experiment 7 application when required.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 2
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
          image: nginx:alpine
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  type: NodePort
  selector:
    app: web-app
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

## Commands

- `kubectl cluster-info` – Displays Kubernetes cluster information.
- `kubectl apply -f deployment.yaml` – Creates or updates resources from the configuration file.
- `kubectl get deployments` – Lists Deployments.
- `kubectl get pods` – Displays pod status.
- `kubectl get services` – Lists Services.
- `kubectl describe deployment web-app` – Displays detailed Deployment information.
- `kubectl logs <pod-name>` – Displays logs from a pod.
- `kubectl scale deployment web-app --replicas=3` – Scales the application to three replicas.
- `kubectl delete -f deployment.yaml` – Deletes the resources defined in the file.

## Expected Output
- Kubernetes creates the Deployment and requests two application replicas.
- The pods reach the Running state if the image is available and the cluster has sufficient resources.
- The Service exposes the application on the configured port.
- The application can be accessed using the appropriate cluster address and NodePort.

## Result
Studied how Kubernetes automates the deployment, scaling, and management of a containerized application using Deployments, pods, and Services.

## Applications
- Automated application deployment
- Container orchestration
- Application scaling
- Service discovery and networking
- DevOps automation
