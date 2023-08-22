---
title: "Jenkins CI/CD Pipeline to deploy a Dockerized Node App on AWS"
datePublished: Tue Aug 22 2023 09:52:12 GMT+0000 (Coordinated Universal Time)
cuid: cllm4n82i00140al55yll2xqt
slug: jenkins-cicd-pipeline-to-deploy-a-dockerized-node-app-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692697599846/cd4d29a4-da22-49c0-8141-e5fa0a7115d3.png
tags: docker, aws, devops, jenkins

---

**Project Overview:**

For this example, we'll use a Node.js web application that serves a "Hello, World!" message. We'll package this application into a Docker container and deploy it to an EC2 instance using Docker Compose.

**Prerequisites:**

1. AWS account with an EC2 instance set up.
    
2. Jenkins server installed and configured.
    
3. Git repository for your web application code.
    

**Sample Declarative Pipeline:**

1. **Create a Dockerfile:**
    

Create a Dockerfile in your application's root directory:

```bash
# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy application code to the container
COPY . .

# Expose the port your application listens on
EXPOSE 3000

# Command to run your application
CMD ["npm", "start"]
```

1. **Create a docker-compose.yml** file:
    

Create a **docker-compose.yml** file in the same directory as your Dockerfile:

```bash
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
```

**Configure Jenkins Pipeline:**

* Create a new pipeline job in Jenkins following the previous instructions.
    
* In the pipeline script section, use the following script as a template:
    

```bash
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: " Github repo URL" , branch: "main"
            }
        }
        
        stage('Build and Package') {
            steps {
                echo "Build the Docker image and tag it"
                sh 'docker build -t my-node-app .'
            }
        }
        
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
```

**Stage: Checkout** In this stage, the pipeline checks out the source code from the specified GitHub repository URL and the main branch. This allows the pipeline to have the latest code to work with.

**Stage: Build and Package** Here, the pipeline builds a Docker image for your Node.js application using the **Dockerfile** in the repository root. The **\-t my-node-app** flag tags the image with the name "**my-node-app**." This image will be used later for deployment.

**Stage: Push to Docker Hub** This stage involves pushing the built Docker image to Docker Hub. The **withCredentials** block is used to securely access Docker Hub credentials stored in Jenkins. The credentials are referenced using the ID **dockerHub**, and the username and password variables are **dockerHubUser** and **dockerHubPass**, respectively. The script tags the previously built image with the Docker Hub username and pushes it to Docker Hub.

**Stage: Deploy** In this final stage, the pipeline handles the deployment of your application using Docker Compose. The script first brings down any existing containers using **docker-compose down** and then starts the application in detached mode (-d) using **docker-compose up -d**.

**Run the Pipeline:**

Save your pipeline configuration and run the pipeline job. Jenkins will execute each stage sequentially, building the Docker image and deploying the application to the EC2 instance using Docker Compose.