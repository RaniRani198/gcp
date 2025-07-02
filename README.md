# 🚀 GCP Cloud Build + GKE: Hello World App Deployment

This project demonstrates a complete CI/CD workflow using **Google Cloud Build**, **Docker**, **Google Kubernetes Engine (GKE)**, and **Kubernetes Service**. It automates the process of building, pushing and deploying a containerized application (`hello-world-app`) with health checks, version control and public access.

---

## 📦 Summary

### 🔧 1. Cloud Build Pipeline

The `cloudbuild.yaml` file automates:

- **Build Docker Image**
  - Builds Docker image from source code.
  - Tags the image with:
    - `latest`: For always deploying the newest version
    - `${_SHORT_SHA}`: For version control, rollback, and debugging

- **Push to Google Container Registry (GCR)**
  - Pushes both `latest` and `${_SHORT_SHA}` image tags to GCR

- **Connect to Kubernetes Cluster (GKE)**
  - Authenticates to the cluster using `gcloud`
  - Gains access to GKE for deployment

- **Deploy to GKE**
  - Updates the Kubernetes Deployment with the newly pushed image
  - Waits until rollout is complete and deployment is healthy

---

### 🐳 2. Kubernetes Deployment Overview

- **Application:** `hello-world-app`
- **Docker Image:** `gcr.io/yourprojectname/hello-world-app:latest`
- **Container Port:** 8080

#### Health Checks

- **Liveness Probe**
  - Ensures the app is running
  - Runs every 10 seconds after initial 10-second delay

- **Readiness Probe**
  - Ensures the app is ready to receive traffic
  - Runs every 5 seconds after initial 5-second delay

---

### 🌐 3. Kubernetes Service Overview

- **Service Type:** LoadBalancer (Exposes app externally)
- **Service Name:** `hello-world-service`
- **Traffic Routing:**
  - External Port: `80`
  - App Port: `8080`

- **Pod Selector:**
  - Uses label `app: hello-world-app` to target the right pods

---

## ✅ Features

- Fully automated CI/CD via Google Cloud Build  
- Tagged Docker images for traceability and rollback  
- Production-ready deployment with Kubernetes probes  
- Exposed service using LoadBalancer for external access  
- Follows GCP best practices for security and efficiency  

---

## 🧰 Prerequisites

- Google Cloud Project with billing enabled  
- GKE cluster created  
- Docker and `gcloud` CLI installed and configured  

Authenticate and connect to your GKE cluster:

```bash
gcloud container clusters get-credentials <CLUSTER_NAME> --zone <ZONE> --project <PROJECT_ID>

---

## 🚀Deploy the App
Submit the build to Cloud Build: gcloud builds submit --config cloudbuild.yaml .
Once complete, get the external IP of the app: kubectl get svc hello-world-service
Open the IP in your browser to view the deployed app.

