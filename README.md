# Go Web Application

This is a simple website written in Golang. It uses the `net/http` package to serve HTTP requests.

## These repository demonstrates a reference architecture. Production deployments require customization based on security, networking, and compliance requirements.

## Running the server Locally

To run the server, execute the following command:

```bash
go run main.go
```

The server will start on port 8080. You can access it by navigating to `http://localhost:8080/courses` in your web browser.

## Looks like this

![Website](static/images/golang-website.png)

## GitHub Actions CI/CD Workflow

This project uses GitHub Actions for CI/CD. The workflow includes steps for building, testing, and deploying the Go application to Kubernetes using Helm.

### Example Workflow Steps

1. **Checkout code**
2. **Set up Go**
3. **Run tests**
4. **Build Docker image**
5. **Push Docker image to registry**
6. **Deploy to Kubernetes using Helm**

See `.github/workflows/` for workflow YAML files.

## Helm Deployment for Go App with Static Files

The Go application and its static files are deployed to Kubernetes using Helm charts. The chart includes configuration for:

- Deployment
- Service
- ConfigMap for static files (if needed)
- Ingress (optional)

### Example Helm Install

```bash
helm install go-web-app ./helm/go-web-app
```

Customize values in `values.yaml` as needed.

## CI/CD Workflow Steps

1. Code pushed to GitHub triggers the workflow.
2. Application is built and tested.
3. Docker image is built and pushed to a container registry.
4. Helm chart is used to deploy or update the application on the Kubernetes cluster.
5. **Create GitHub Actions secrets for Docker registry credentials and GitHub token to allow pushing Docker images and committing changes to Helm values.**  
TOKEN, DOCKERHUB_TOKEN, DOCKERHUB_USERNAME

## Prerequisites

- An EKS cluster must be created with worker nodes ready for deployments.
- An NGINX Ingress controller must be set up in the cluster to enable public access to the application.

### Example NGINX Ingress Controller Install

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/aws/deploy.yaml
```

- Install ArgoCD in a new namespace (e.g., `argocd`) and create an ArgoCD project to manage Helm chart updates upon pipeline completion.

### Example ArgoCD Install

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Refer to ArgoCD documentation for project and application setup to automate Helm updates.


