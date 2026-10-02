# Task 2 - Simple Jenkins Pipeline for CI/CD

## Objective

Create a simple Jenkins pipeline to automate the process of building, testing, and deploying an application using Jenkins and Docker.

## Tools Used

* Jenkins
* Docker
* GitHub
* Nginx

## Project Structure

```text
jenkins-cicd-task-2/
├── Dockerfile
├── Jenkinsfile
├── README.md
└── index.html
```

## Jenkins Pipeline Stages

The Jenkins pipeline contains three stages:

### 1. Build

Builds the Docker image using the project Dockerfile.

```bash
docker build -t jenkins .
```

### 2. Test

Runs the Docker container temporarily and checks whether the application is accessible.

```bash
docker run --rm -d --name jenkins-test -p 8082:80 jenkins
```

### 3. Deploy

Stops the previous application container and deploys a new container.

```bash
docker rm -f jenkins-container || true
docker run -d --name jenkins-container -p 8081:80 jenkins
```

## Application

The application is a simple HTML webpage served using Nginx inside a Docker container.

The deployed application runs on:

```text
http://localhost:8081
```

## Jenkins

Jenkins was installed locally and configured to run the CI/CD pipeline.

Jenkins URL:

```text
http://localhost:8080
```

## Result

The Jenkins pipeline successfully completed the following stages:

```text
Build → Test → Deploy
```

The Docker application was successfully built, tested, and deployed using Jenkins.

## Conclusion

This task demonstrates a basic CI/CD workflow using Jenkins and Docker, including automated Docker image building, application testing, and deployment.
