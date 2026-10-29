Output

Kubernetes creates the Deployment and requests two application replicas.

The pods reach the Running state if the image is available and the cluster has sufficient resources.

The Service exposes the application on the configured port.

The application can be accessed using the appropriate cluster address and NodePort.
