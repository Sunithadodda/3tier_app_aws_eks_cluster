# Deploy a 3-Tier App on Amazon EKS Cluster

## Overview

This project demonstrates the development, containerization, deployment, and continuous integration (CI) and continuous delivery (CD) of a 3-tier web application. The application is built using:

- **Backend**: .NET Core
- **Frontend**: HTML, CSS, and JavaScript
- **Database**: PostgreSQL

The project is structured into four parts:

1. **Containerization of Microservices**: Dockerize the frontend, backend, and database.
2. **Kubernetes Deployment**: Deploy the application on Kubernetes (Amazon EKS).
3. **Continuous Integration (CI)**: Implement a CI pipeline using GitHub Actions.
4. **Continuous Delivery (CD)**: Implement a CD pipeline to deploy the application to Amazon EKS.

## Pre-requisites

Before you start, make sure you have the following:

- A **host machine** with **Docker** and a **Kubernetes cluster** (EKS) installed.
- An **AWS account** with valid IAM user permissions.
- Basic knowledge of Docker, Kubernetes, and GitHub Actions.

## Project Structure

- `Basic3Tier.API`: Backend application code (built using .NET Core).
- `Basic3Tier.UI`: Frontend application code (HTML, CSS, JavaScript).
- `PostgreSQL`: Database used in the project.

## Containerize All Microservices

In this part, we containerize the frontend, backend, and database applications using Docker.

### Steps:

1. **Create Docker Images**: 
   - Frontend, Backend, and PostgreSQL containers should be created using Dockerfiles.
   - Ensure that Docker network settings are configured to allow communication between the containers.
   
2. **Run the Application Locally**:
   - Deploy the containers locally using Docker and verify the application is running successfully.
   

## Deploy the Application on Kubernetes

In this part, we deploy the containerized application on Kubernetes (Amazon EKS).

### Steps:

1. **Deployment Manifests**:
   - Create Kubernetes manifests for the frontend, backend, and PostgreSQL services.
   - Deploy the frontend (1 pod), backend (3 pods), and database (1 pod).

2. **Service Configuration**:
   - Create a **NodePort** service for the frontend and backend applications.
   - Create **ClusterIP** services to connect the frontend and backend, and the backend with PostgreSQL.
   - Use **Persistent Volume** on Amazon EFS to store PostgreSQL data.
   - Set up a **Load Balancer** to expose the frontend application.


## Continuous Integration (CI)

In this part, we implement a CI pipeline using **GitHub Actions**.

### Steps:

1. **Build, Test, and Scan**:
   - Add a step to build, test, and scan the frontend and backend code.
   
2. **Create Docker Images**:
   - Add steps to create Docker images for both frontend and backend.
   - Push these images to **Docker Hub**.
   
3. **Deploy Using Manifests**:
   - Include Kubernetes manifests for creating deployments and services in the pipeline.

## Continuous Delivery (CD)

In this part, we implement a CD pipeline to deploy the application to Amazon EKS.

### Steps:

1. **Connect to EKS Cluster**:
   - Add steps to connect to the **Amazon EKS** cluster using the correct IAM permissions.

2. **Deploy Using kubectl**:
   - Use `kubectl apply` commands in the pipeline to deploy all Kubernetes deployments and services.

3. **Verify Application**:
   - Ensure that the application is running successfully on the EKS cluster.

## Setting Up the Project

### Docker Setup

1. Build and run the Docker containers:

   ```bash
   docker build -t dsunitha/new_frontend .
   docker build -t dsunitha/new_frontend .

2. Push the Docker images:
   
   ```bash
   docker push dsunitha2/new_backend
   docker push dsunitha2/new_frontend
   
### Kubernetes Setup
1. Ensure you have a Kubernetes cluster (EKS) running and kubectl is configured.

2. Apply the Kubernetes manifests:
   
   ```bash
   kubectl apply -f backend-deployment.yml --validate=false
          kubectl apply -f backend-service.yml --validate=false
          kubectl apply -f database-deployment.yml --validate=false
          kubectl apply -f database-service.yml --validate=false
          kubectl apply -f docker-compose.yml --validate=false
          kubectl apply -f frontend-deployment.yml --validate=false
          kubectl apply -f frontend-ingress.yml --validate=false
          kubectl apply -f frontend-lb-service.yml --validate=false
          kubectl apply -f frontend-service.yml --validate=false
          kubectl apply -f postgres-pv.yml --validate=false
          kubectl apply -f postgres-pvc.yml --validate=false

3. Ensure pods are running:

  ```bash
   kubectl get pods
   kubectl get services

### Github Actions Setup

Set up GitHub Actions by creating a  .github/workflows/ci.yml file with the necessary steps.

1. Building and testing code.
2. Creating Docker images and pushing to Docker Hub.
3. Deploying the application to EKS
