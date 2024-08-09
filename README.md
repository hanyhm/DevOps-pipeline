# Vidly DevOps Project

## Introduction

This project demonstrates a comprehensive DevOps pipeline for the Vidly application, a video rental platform. It showcases the implementation of modern DevOps practices and tools, focusing on automation, continuous integration, continuous deployment, and monitoring.

The pipeline is designed to streamline the development process, ensure code quality, enable rapid and reliable deployments, and provide robust monitoring capabilities.

## Project Scope

This project encompasses:

1. Source Code Management using GitHub
2. Containerization of the application using Docker
3. Continuous Integration (CI) using GitHub Actions
4. Container Registry management with Docker Hub
5. Continuous Deployment (CD) using Jenkins
6. Orchestration with Kubernetes
7. Monitoring and observability with Prometheus and Grafana

## Architecture

<img src="./diagram.png" alt="Project Diagram" width="700" height="400">

The Vidly application consists of three main components:

1. Frontend: A React-based web application
2. Backend: A Node.js API server
3. Database: MongoDB for data storage

These components are containerized and deployed to a Kubernetes cluster. The entire system is monitored using Prometheus and Grafana.



## Technologies Used

- Version Control: GitHub
- Programming Languages: JavaScript (Node.js, React)
- Containerization: Docker
- CI/CD: GitHub Actions, Jenkins
- Orchestration: Kubernetes
- Monitoring: Prometheus, Grafana
- Database: MongoDB


## Project Structure

```bash
vidly/
├── frontend/
│   ├── Dockerfile
│   └── ... (React app files)
├── backend/
│   ├── Dockerfile
│   └── ... (Node.js app files)
├── k8s/
│   ├── frontend-deployment.yaml
│   ├── backend-deployment.yaml
│   ├── mongodb-deployment.yaml
│   ├── prometheus-config.yaml
│   └── grafana-deployment.yaml
├── .github/
│   └── workflows/
│       └── ci.yml
├── Jenkinsfile
└── README.md
```

## CI/CD Pipeline

1. **Code Commit**: Developers push code to the GitHub repository.
2. **Continuous Integration**: 
   - GitHub Actions triggers automated tests for both frontend and backend.
   - If tests pass, Docker images are built and pushed to Docker Hub.
3. **Continuous Deployment**:
   - Jenkins pulls the latest images and deploys to the Kubernetes cluster.
4. **Monitoring**:
   - Prometheus continuously collects metrics from the deployed applications.
   - Grafana provides visualization of these metrics.

## Setup Instructions

### 1. Clone the repository:
```bash
git clone https://github.com/hanyhm/vidly.git
```

### 2. Set up Docker Hub credentials in GitHub Secrets:
```bash
- DOCKERHUB_USERNAME
- DOCKERHUB_PASSWORD
```

### 3. Set up a Kubernetes cluster (you can use Minikube for local testing).

### 4. Install and configure Jenkins:
- Ensure Jenkins has access to your Kubernetes cluster.
- Create a Jenkins credential for your kubeconfig file.

### 5. Create a Jenkins job that uses the Jenkinsfile in the repo.

### 6. Set up a GitHub webhook to trigger the Jenkins job on push to the main branch.

### 7. Deploy Prometheus and Grafana:
```bash
kubectl apply -f k8s/prometheus-config.yaml
kubectl apply -f k8s/grafana-deployment.yaml
```

8. Access Grafana and set up dashboards to visualize your application metrics.

## Usage

- Push changes to the main branch to trigger the CI/CD pipeline.
- Monitor the GitHub Actions workflow and Jenkins job for deployment status.
- Access the application.
- View application metrics and performance in Grafana.

## Monitoring

- Prometheus is set up to scrape metrics from all Kubernetes pods.
- Grafana provides visualization of these metrics.
- Default dashboards include:
- Kubernetes cluster overview
- Node.js application metrics
- MongoDB performance metrics

## Commands to test App

### 1. Clone the repository:
```bash
git clone https://github.com/hanyhm/vidly.git
```
### 2. CD into repo and run test
```bash
cd vidly
cd frontend
npm test
cd ..
cd backend
npm test
```
### 3. Use Docker compose to run app in Docker
ps. You must have Docker & Docker compose installed on your machine

```bash
cd vidly
docker compose up -d
```
check app at http://localhost:3000

### 4. Ttrigger CI

Make a change to the source code and watch GitHub Actions workflow to test and update docker images of the application.

<img src="./img/actions.png" alt="Project Diagram" width="700" height="150">


This DevOps Pipeline Showcase Project demonstrates the ability to design, implement, and manage
a modern, cloud-native application lifecycle.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details.

