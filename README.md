# Todo App --- CI/CD & GitOps on AWS

An end-to-end DevOps project deploying a React + FastAPI Todo application to Amazon EKS using Terraform, Jenkins, Docker Hub, Argo CD, and Argo CD Image Updater.


## Architecture

``` mermaid
flowchart TD
    A[Application source<br/>React + FastAPI] --> B[Jenkins CI pipeline]
    B --> C[Build container images]
    C --> D[Docker Hub<br/>Frontend and backend images]
    D --> E[Argo CD Image Updater]
    E --> F[GitOps repository<br/>Kustomize image tags]
    F --> G[Argo CD]
    G --> H[Amazon EKS]
    H --> I[Kubernetes Deployments and Services]
    I --> J[AWS Load Balancer Controller]
    J --> K[Application Load Balancer]
    K --> L[Todo application in browser]
    T[Terraform-managed AWS infrastructure] --> H
```

## Tech Stack

-   **Frontend:** React
-   **Backend:** FastAPI
-   **Containers:** Docker
-   **CI:** Jenkins and a Jenkins Shared Library
-   **Container Registry:** Docker Hub
-   **GitOps / CD:** Argo CD and Argo CD Image Updater
-   **Orchestration:** Kubernetes on Amazon EKS
-   **Networking:** AWS Load Balancer Controller and Application Load
    Balancer
-   **Infrastructure as Code:** Terraform

## How It Works

1.  Application source code is stored in the application repository.
2.  Jenkins checks out the code, validates required files, builds
    frontend and backend Docker images, and pushes them to Docker Hub.
3.  Argo CD Image Updater detects eligible image versions and updates
    the image tags in the GitOps configuration.
4.  Argo CD detects the Git change and synchronizes the Kubernetes
    resources in Amazon EKS.
5.  The AWS Load Balancer Controller manages the Application Load
    Balancer, which routes browser traffic to the application.

## Screenshots

### 1. Application Running

![Todo application running](screenshots/app.png)

### 2. Jenkins CI Pipeline

![Successful Jenkins pipeline](screenshots/ci_pipeline.png)

### 3. Docker Hub Images

![Frontend and backend Docker images on Docker
Hub](screenshots/dockerhub.png)

### 4. Argo CD Application Status

![Argo CD application status](screenshots/argo_ui.png)

### 5. Argo CD Image Updater

![Image updater updating the GitOps image
tag](screenshots/image_updater.png)

### 6. Terraform State

![Terraform state list showing managed
resources](screenshots/state_list.png)

### 7. AWS and Kubernetes Resources

![AWS infrastructure and Kubernetes
resources](screenshots/resources.png)

## Related Repositories

-   **GitOps / Kubernetes manifests:**
    [todo-app-argo-cd](https://github.com/sakshamjp2004/todo-app-argo-cd)
-   **Application source and CI pipeline:**
    [react-fastapi-todo](https://github.com/sakshamjp2004/react-fastapi-todo)
-   **Reusable Jenkins Shared Library:**
    [todo-sharedLibrary](https://github.com/sakshamjp2004/todo-sharedLibrary)

## Key Learnings

-   Building and publishing multi-service Docker images through Jenkins.
-   Reusing pipeline logic with a Jenkins Shared Library.
-   Deploying applications to Amazon EKS.
-   Managing Kubernetes deployments through GitOps with Argo CD.
-   Automating image-tag updates with Argo CD Image Updater.
-   Exposing an application using AWS Load Balancer Controller and an
    Application Load Balancer.
-   Using Terraform to manage cloud infrastructure.

------------------------------------------------------------------------

