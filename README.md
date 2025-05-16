# DevOps W04 In-Class Exercise Template

This repository contains a full-stack application with a SvelteKit client and a Spring Boot server. It demonstrates modern web application architecture and DevOps practices.

## Project Overview

This project includes:
- **Client**: SvelteKit with TypeScript, TailwindCSS, and reusable UI components.
- **Server**: Spring Boot Java application with RESTful APIs.
- **DevOps**: Dockerized services, CI/CD pipelines, and production-ready deployment configurations.

## Prerequisites

- Node.js (v22 or later)
- Java JDK 21+
- Gradle
- Docker and Docker Compose
- **Docker Desktop with Kubernetes**
- Git

## Setup Instructions

### Clone the Repository

```bash
git clone https://github.com/yourusername/w04-template.git
cd w04-template
```

### Client Setup

1. Navigate to the `client` directory:
   ```bash
   cd client
   ```
2. Install dependencies:
   ```bash
   npm install
   ```

### Server Setup

1. Navigate to the `server` directory:
   ```bash
   cd server
   ```
2. Build the project:
   ```bash
   ./gradlew build
   ```

## Running the Application

### Start the Client

```bash
cd client
npm run dev
```
The client will be available at [http://localhost:3000](http://localhost:3000).

### Start the Server

```bash
cd server
./gradlew bootRun
```
The server API will be available at [http://localhost:8080](http://localhost:8080).

## Development Workflow

### Client Development

- Built with SvelteKit and TypeScript for a modern, reactive UI.
- TailwindCSS for styling.
- Components and routes are organized in the `src` directory.

### Server Development

- Built with Spring Boot for scalable and maintainable server services.
- Gradle is used for dependency management and building.
- Source code is in the `src/main/java` directory.
- Tests are in the `src/test/java` directory.

## Building for Production

### Client Build

```bash
cd client
npm run build
```

### Server Build

```bash
cd server
./gradlew clean build
```

## Dockerized Deployment

The project includes Docker configurations for containerized deployment.

### Build and Run with Docker Compose

1. Build and start the services:
   ```bash
   docker compose up --build
   ```
2. Access the application:
   - Client: [http://localhost:3000](http://localhost:3000)
   - Server: [http://localhost:8080](http://localhost:8080)

## Kubernetes Deployment

This project can be deployed to a Kubernetes cluster. The Kubernetes configuration files are located in the `k8s` directory.

### Ensure Docker Desktop Kubernetes is Active

Before deploying, make sure you're using Docker Desktop's Kubernetes:

1. Verify that Kubernetes is enabled in Docker Desktop:
   - Open Docker Desktop
   - Go to Settings/Preferences
   - Select "Kubernetes" from the left menu
   - Check "Enable Kubernetes"
   - Click "Apply & Restart" if needed

2. Confirm Docker Desktop is your current kubectl context:
   ```bash
   kubectl config current-context
   ```
   This should return `docker-desktop` or similar.

3. If needed, switch to Docker Desktop context:
   ```bash
   kubectl config use-context docker-desktop
   ```

### Deploy to Local Kubernetes

Follow these steps to deploy the application correctly:

1. Create the namespace and deploy all resources at once:
   ```bash
   kubectl apply -f k8s/namespace.yaml
   kubectl apply -f k8s
   ```

2. Check the status of all deployed resources:
   ```bash
   kubectl -n canteen-app get all
   ```

3. Verify services are running with the correct ports:
   ```bash
   kubectl -n canteen-app get service
   ```
   You should see the client service using NodePort 30000 and the server service using NodePort 30001.

4. Wait for all pods to be in the running state:
   ```bash
   kubectl -n canteen-app get pods
   ```

### Accessing the Application

After successful deployment, you can access:

- The client application at: http://localhost:30000
- The server API directly at: http://localhost:30001

The client is already configured to communicate with the server through the fixed NodePort 30001 as defined in the ConfigMap.

## CI/CD Pipeline

The project includes GitHub Actions workflows for:
- **Building Docker Images**: Automatically builds and pushes Docker images to GitHub Container Registry.
- **Deploying Docker Images**: Deploys the application to a production environment using Docker Compose.

## Project Structure

```
├── client/                  # SvelteKit client
│   ├── src/                 # Source code
│   ├── public/              # Static assets
│   └── package.json         # Client dependencies
│
├── server/                  # Spring Boot server
│   ├── src/                 # Source code
│   ├── build.gradle         # Gradle build file
│   └── Dockerfile           # Server Dockerfile
│
├── k8s/                     # Kubernetes configuration files
│   ├── client-deployment.yaml
│   ├── client-service.yaml
│   ├── server-deployment.yaml
│   ├── server-service.yaml
│   ├── configmap.yaml
│   └── namespace.yaml
│
├── compose.yml              # Docker Compose for local development
└── .github/workflows/       # CI/CD workflows
```

## License

This project is licensed under the MIT License.