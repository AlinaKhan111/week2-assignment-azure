# **Task**: Create Container Instance and Deploy a Simple Docker Application
## Objective
Deploy a Docker application using Azure Container Instances (ACI).

## Steps Performed
### 1.Created a Container Instance

- Opened Azure Portal > Searched for Container Instances > Clicked Create.

- Configured:

  - Container Name (e.g., simpleapp-container)

  - Resource Group

  - Region

  - Image source: Docker Hub

  - Image: e.g., nginx, hello-world, or custom image

  - Port: 80 (for web access, if required)

  - DNS Name Label (optional, for easy browser access)

### 2.Deployed the Container

- Waited for the deployment to complete.

### 3.Tested the Deployment

- Accessed the container via Public IP or FQDN.

- Verified that the application (e.g., Nginx welcome page) was running.

## Outcome
A Docker application was successfully deployed and verified using Azure Container Instances.