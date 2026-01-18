# AWS EKS Deployment Template

This repository provides a **reference DevOps template** for deploying a containerized application to **Amazon EKS** using **Helm** and **CI/CD automation**.

The goal of this project is to demonstrate a **reproducible, maintainable, and deployment-ready setup** suitable for real-world enterprise environments.

---

## Purpose

This repository is designed to:

- Demonstrate Kubernetes application deployment on AWS EKS
- Use **Helm charts** for configuration and release management
- Provide a structured foundation for CI/CD pipelines
- Follow infrastructure and deployment best practices
- Serve as a reusable template for future projects

The focus is on **clarity, stability, and documentation**, not on complexity.

---

## Architecture Overview

High-level flow:

1. Application is containerized using Docker  
2. Image is pushed to a container registry  
3. Kubernetes resources are defined using Helm  
4. Application is deployed to an existing EKS cluster  
5. CI/CD automates build and deployment steps  

---

## Repository Structure

```
.
├── .github/workflows/        # CI/CD pipelines (GitHub Actions)
├── helm/                     # Helm charts for application deployment
├── k8s/                      # Kubernetes manifests (if applicable)
├── static/                   # Static application assets
├── Dockerfile                # Docker image definition
├── main.go                   # Sample application source
├── main_test.go              # Unit tests
└── README.md                 # Project documentation
```

---

## Prerequisites

Ensure the following tools and resources are available:

- AWS account with an existing **EKS cluster**
- kubectl configured for cluster access
- Helm 3.x installed
- Docker installed
- Container registry (Docker Hub or Amazon ECR)
- GitHub repository with required secrets configured

---

## Build and Run Locally

### Build Docker Image

```bash
docker build -t <registry>/go-web-app:latest .
```

### Run Locally

```bash
docker run -p 8080:8080 <registry>/go-web-app:latest
```

---

## Deployment to EKS Using Helm

### Install / Upgrade Release

```bash
helm upgrade --install go-web-app ./helm/go-web-app-chart \
  --set image.repository=<registry>/go-web-app \
  --set image.tag=latest
```

Verify deployment:

```bash
kubectl get pods
kubectl get svc
```

---

## CI/CD Pipeline

The CI/CD pipeline automates:

1. Code checkout
2. Build and test execution
3. Docker image build
4. Image push to container registry
5. Deployment to EKS using Helm

### Required GitHub Secrets

| Secret Name              | Description                          |
|--------------------------|--------------------------------------|
| AWS_ACCESS_KEY_ID        | AWS access key                       |
| AWS_SECRET_ACCESS_KEY   | AWS secret key                       |
| AWS_REGION              | AWS region of EKS cluster            |
| DOCKER_USERNAME         | Container registry username          |
| DOCKER_PASSWORD         | Container registry access token      |

Pipeline definitions are located under `.github/workflows/`.

---

## Design Decisions

- **Helm** is used to manage Kubernetes deployments consistently across environments  
- Configuration is externalized to support environment-specific values  
- CI/CD focuses on repeatability and traceability  
- The structure prioritizes long-term maintainability over quick demos  

---

## Future Improvements

Potential enhancements include:

- GitOps deployment using Argo CD
- Environment promotion (dev → staging → prod)
- Monitoring with Prometheus and Grafana
- Security scanning and policy enforcement
- Ingress with TLS termination

---

## Intended Audience

This repository is intended for:

- DevOps and Platform Engineers
- Engineers learning Kubernetes and Helm on AWS
- Reference implementations for enterprise DevOps interviews
- Reusable internal deployment templates

---

## License

This project is provided as a reference template and is free to use and adapt.

---

## Author

Maintained as a learning and reference project focused on **enterprise-grade DevOps practices**.
