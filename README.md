# Continuous Delivery with Jenkins in Kubernetes Engine

This repository contains the resources and configuration files I used while completing the **Qwiklabs** lab **“Continuous Delivery with Jenkins in Kubernetes Engine”**.  
It demonstrates setting up a complete CI/CD pipeline using **Jenkins**, **Docker**, and **Google Kubernetes Engine (GKE)**.

---

## Overview

The lab walks through:

1. **Provisioning a GKE Cluster** – Creating a Kubernetes Engine cluster on Google Cloud.  
2. **Deploying Jenkins on GKE** – Installing Jenkins with persistent storage and service exposure.  
3. **Creating a Sample App** – A simple Go/HTML web app packaged in a Docker image.  
4. **Configuring a CI/CD Pipeline** – Using a `Jenkinsfile` to:
   - Build and containerize the app
   - Push the Docker image to **Google Container Registry (GCR)**
   - Deploy the updated app to the GKE cluster.

---

## Project Structure

<pre lang="markdown">  ├── Dockerfile # Docker build instructions for the sample app 
  ├── Jenkinsfile # Declarative pipeline definition 
  ├── html.go # Simple HTML handler (Go web app) 
  ├── main.go # Go application entry point 
  ├── k8s/ 
  │ ├── deployment.yaml # Kubernetes Deployment manifest 
  │ └── service.yaml # Kubernetes Service manifest 
  └── vendor/ # Go dependencies (if using dep) </pre>


---

## Prerequisites

To replicate this lab you’ll need:

* A **Google Cloud Platform (GCP)** project  
* **gcloud** CLI  
* **kubectl** CLI  
* **Docker**  
* **Go** (if you want to build locally)

---

## Running Locally

```bash
# Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# Build and run locally
go build -o app .
./app
```

## Deploying to GKE

```bash
# Build Docker image
docker build -t gcr.io/<PROJECT_ID>/cd-jenkins-gke:v1 .

# Push to GCR
docker push gcr.io/<PROJECT_ID>/cd-jenkins-gke:v1

# Apply Kubernetes manifests
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```
## CI/CD Pipeline

The `Jenkinsfile` automates:

1. Pulling code from GitHub
2. Building the Docker image
3. Pushing the image to GCR
4. Triggering a rolling update on the GKE deployment

---

## License

This repository follows the license of the original Qwiklabs content (for personal/educational use).

---

## References

* [Qwiklabs: Continuous Delivery with Jenkins in Kubernetes Engine](https://www.qwiklabs.com/)
* [Google Cloud Kubernetes Engine](https://cloud.google.com/kubernetes-engine)
* [Jenkins Documentation](https://www.jenkins.io/doc/)
