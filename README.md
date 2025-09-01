# SampleAPI - .NET Application CI/CD Pipeline Documentation

## Application Overview

SampleAPI is a RESTful API built with ASP.NET Core (.NET 8). It provides endpoints for weather forecasting and product administration, and is containerized for deployment to Azure App Service.

## Key Components Created

- **.NET API Project**: ASP.NET Core Web API (SampleAPI)
- **Dockerfile**: For containerizing the application
- **azure-pipelines.yml**: Azure DevOps pipeline for CI/CD
- **Self-hosted Runner**: Azure VM (Linux/Windows) configured as a build agent(SampleAPIVMPool)
- **Azure Container Registry (ACR)**: Stores built Docker images
- **Azure App Service (sampleapi-app)**: Hosts the deployed container
- **Branching Strategy**: main (production), feature (development)

## Workflow Steps

1. **Development**
   - Code is developed in the `feature` branch.
   - Once ready, a pull request is created to merge changes into `main`.

2. **Pull Request & Approval**
   - PR is reviewed and approved.
   - Upon approval, code is merged into `main`.

3. **CI/CD Pipeline Trigger**
   - Pipeline triggers only on changes to `main`.
   - No builds or deployments from `feature` branch.

4. **Build & Publish**
   - .NET SDK is installed on the agent (self-hosted runner on Azure VM).
   - Project is built and published.
   - Docker image is built from published output.
   - Image is pushed to ACR.

5. **Deployment**
   - Docker image is deployed from ACR to Azure App Service (`sampleapi-app`).
   - Only `main` branch triggers deployment.

## Self-hosted Runner Details

- **Agent Pool**: SampleAPIVMPool
- **VM Host**: Azure VM (see screenshot)
- **OS**: Linux/Windows (as configured)
- **Purpose**: Runs pipeline jobs for build, publish, Docker, and deployment steps

## Pipeline Details

- Installs .NET 8 SDK
- Builds and publishes the .NET project
- Builds Docker image from published output
- Pushes Docker image to ACR
- Deploys image to Azure App Service

## Screenshots

### 1. Azure App Service Overview
![Azure App Service Overview](attachments/0)

### 2. Azure DevOps Repo Structure
![Azure DevOps Repo Structure](attachments/1)

### 3. Swagger UI (Deployed API)
![Swagger UI](attachments/2)

### 4. Pipeline Build Steps
![Pipeline Build Steps](attachments/3)

### 5. Pipeline Run History
![Pipeline Run History](attachments/4)

### 6. Pull Request Approval
![Pull Request Approval](attachments/5)

### 7. Agent Pool
![Agent Pool](attachments/6)

### 8. VM Details (Agent Host)
![VM Details](attachments/7)

