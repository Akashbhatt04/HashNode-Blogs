---
title: "How to Create a Docker Container."
seoTitle: "How to Create a Docker Container."
seoDescription: "How to Create a Docker Container."
datePublished: Sun Apr 09 2023 18:49:58 GMT+0000 (Coordinated Universal Time)
cuid: clg9res6k000u09jt1twl11e0
slug: how-to-create-a-docker-container
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/jOqJbvo1P9g/upload/a04cad99729b11595d9640ecba79e727.jpeg
tags: docker, devops, docker-container

---

**To create a container, you will need to follow these general steps:**

1. Choose a containerization platform: There are several containerization platforms to choose from, such as Docker, Kubernetes, and Podman. Choose a platform that suits your needs.
    
2. Create a Dockerfile: If you're using Docker, you'll need to create a Dockerfile that defines the container's environment and configuration. The Dockerfile is a text file that contains instructions on how to build the container.
    
3. Build the container image: Once you have created the Dockerfile, you can use it to build the container image. This involves running the docker build command, which reads the Dockerfile and creates a container image.
    
4. Run the container: Once you have created the container image, you can run it using the docker run command. This will start the container and run the application or service that you have configured in the Dockerfile.
    

**Here is an example Dockerfile:**

```plaintext
FROM ubuntu:latest 
RUN apt-get update && apt-get install -y nginx 
COPY index.html /var/www/html/
EXPOSE 80 
CMD ["nginx", "-g", "daemon off;"]
```

This Dockerfile installs the Nginx web server and copies an HTML file to the server's document root. The EXPOSE command exposes port 80, and the CMD command starts the Nginx server.

To build and run the container using this Dockerfile, you would run the following commands:

```plaintext
docker build -t my-nginx-image . 
docker run -p 80:80 my-nginx-image
```

**The first command builds the container image using the Dockerfile in the current directory and tags it with the name my-nginx-image. The second command runs the container and maps port 80 on the host to port 80 in the container.**