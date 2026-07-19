# Java Maven Web Application

## 📌 Overview

This repository contains a sample Java Maven web application used to demonstrate an end-to-end CI/CD pipeline.

The application is built using Maven, containerized with Docker, and deployed to Kubernetes using a Jenkins pipeline.

---

## 🚀 Tech Stack

- Java
- Maven
- Apache Tomcat
- Docker
- Jenkins
- SonarQube
- Docker Hub
- Kubernetes (Minikube)

---

## 📁 Project Structure

```
java-maven-webapp/
├── src/
├── pom.xml
├── Dockerfile
├── Jenkinsfile
└── README.md
```

---

## ⚙️ Build the Application

Clone the repository:

```bash
git clone https://github.com/Kunal-18L/java-maven-webapp.git
cd java-maven-webapp
```

Build using Maven:

```bash
mvn clean package
```

The WAR file will be generated in the `target/` directory.

---

## 🐳 Build Docker Image

```bash
docker build -t java-maven-webapp:latest .
```

Run the container:

```bash
docker run -d -p 8080:8080 java-maven-webapp:latest
```

---

## 🔄 Jenkins Pipeline

The Jenkins pipeline performs the following steps:

1. Clone the GitHub repository
2. Build the application using Maven
3. Perform SonarQube code analysis
4. Build the Docker image
5. Push the Docker image to Docker Hub

---

## 📦 Docker Hub Repository

Docker Image:

```
kunal18l/java-maven-webapp:latest
```

---

## ☸️ Kubernetes Deployment

The Docker image can be deployed to Kubernetes using the deployment and service manifests available in the **devops-automation** repository.

---

## 👨‍💻 Author

**Karan**

GitHub: https://github.com/Kunal-18L
