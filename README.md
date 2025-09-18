# Continuous Delivery with Jenkins on Google Kubernetes Engine (GKE)

[![Go](https://img.shields.io/badge/Go-1.21%2B-blue)](https://golang.org/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-1.27%2B-brightgreen)](https://kubernetes.io/)
[![Jenkins](https://img.shields.io/badge/Jenkins-2.4%2B-orange)](https://www.jenkins.io/)

A reference implementation of **Continuous Delivery (CD)** using **Jenkins**, **Docker**, and **Google Kubernetes Engine (GKE)**.  
This project is based on the **Qwiklabs** lab *“Continuous Delivery with Jenkins in Kubernetes Engine”*.

---

## Features

- **Automated CI/CD Pipeline** using a declarative `Jenkinsfile`.
- **Google Kubernetes Engine Deployment** with rolling updates.
- **Dockerized Go Web App** for demonstration.
- Includes Kubernetes manifests (`deployment.yaml`, `service.yaml`) and Dockerfile.

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

Before running or deploying, ensure you have:

- **Google Cloud Platform (GCP) Project** with billing enabled
- [gcloud CLI](https://cloud.google.com/sdk/docs/install)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Docker](https://docs.docker.com/get-docker/)
- [Go](https://golang.org/) (v1.21 or newer)
- [Jenkins](https://www.jenkins.io/) (if running pipeline locally or on a server)

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Harsimran-Dalal/Continuous-Delivery-jenkins-gke.git
cd Continuous-Delivery-jenkins-gke
```
## 2. Running Locally

```bash
# Build and run locally
go build -o app .
./app
```
Access the app at http://localhost:8080

## 3. Build and Push Docker Image

```bash
docker build -t gcr.io/<PROJECT_ID>/cd-jenkins-gke:v1 .
docker push gcr.io/<PROJECT_ID>/cd-jenkins-gke:v1
```
Replace <PROJECT_ID> with your actual GCP project ID.


## 4. Deploying to GKE

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

## Jenkins CI/CD Pipeline

The `Jenkinsfile` automates:

1. Pulling code from GitHub
2. Building the Docker image
3. Pushing the image to GCR
4. Rolling update to the Kubernetes cluster
Configure a Jenkins job to use this pipeline file.
---

## Testing

Run unit tests:
```bash
go test ./...
```
---

## Configuration

If environment variables are required, create a `.env` file or set them in your deployment manifests.
Example variables:
```bash
PROJECT_ID=<your-gcp-project>
IMAGE_TAG=v1
```
---

## Contributing

Contributions are welcome!

1. Fork the repository
2. Create a new branch: git checkout -b feature/YourFeature
3. Commit changes: git commit -m "Add new feature"
4. Push to branch: git push origin feature/YourFeature
5. Open a Pull Request
---

## License

This repository follows the license of the original Qwiklabs content (for personal/educational use).

---

## References

* [Qwiklabs: Continuous Delivery with Jenkins in Kubernetes Engine](https://www.qwiklabs.com/)
* [Google Cloud Kubernetes Engine](https://cloud.google.com/kubernetes-engine)
* [Jenkins Documentation](https://www.jenkins.io/doc/)
