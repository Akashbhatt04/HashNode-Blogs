---
title: "What is JENKINS ? And what are the various method to install it ?"
seoTitle: "What is JENKINS ? And what are the various method to install it ?"
seoDescription: "What is JENKINS ? And what are the various method to install it ?"
datePublished: Sun Apr 16 2023 17:17:30 GMT+0000 (Coordinated Universal Time)
cuid: clgjo6twa000e09kwgdnzdelo
slug: what-is-jenkins-and-what-are-the-various-method-to-install-it
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681665307360/96b5a746-71cd-4386-9b71-4b25cbc003b3.jpeg
tags: docker, devops, jenkins

---

Jenkins is an open-source automation server that helps automate software development processes such as building, testing, and deploying software. Jenkins is widely used by developers and organizations to streamline their software development workflows and improve the speed and quality of their software releases.

### To install Jenkins, follow these steps:

1. **Download Jenkins**: Go to the Jenkins website and download the latest version of Jenkins. You can choose to download the installation package for your operating system, or download the generic WAR (Web Application Archive) file if you prefer to deploy Jenkins in a servlet container.
    
2. **Install Java**: Jenkins is a Java-based application, so you need to install the Java Development Kit (JDK) before you can run Jenkins. You can download and install the JDK from the Oracle website.
    
3. **Install Jenkins**: Once you have downloaded the Jenkins installation package or WAR file, follow the instructions for your operating system to install Jenkins. If you downloaded the WAR file, you need to deploy it to a servlet container such as Tomcat or Jetty.
    
4. **Launch Jenkins**: Once Jenkins is installed, launch it by opening a web browser and navigating to the URL where Jenkins is running. The default URL for Jenkins is [http://localhost:8080](http://localhost:8080).
    
5. **Configure Jenkins**: After launching Jenkins, you need to configure it to your specific needs. This includes setting up security, plugins, and other settings. Jenkins provides a web-based interface for configuring the server.
    

### Install Jenkins using Docker:-

1. **Install Docker**: If you haven't already, install Docker on your system.
    
2. **Pull the Jenkins image**: Open your terminal or command prompt and type the following command to pull the Jenkins image from Docker Hub:
    

```plaintext
docker pull jenkins/jenkins:lts
```

This will download the latest Jenkins image with the LTS tag.

1. **Start a Jenkins container**: After downloading the Jenkins image, start a new container with the following command:
    

```plaintext
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

This command will start a new container with the Jenkins image, bind port 8080 and 50000 to the host, and create a persistent volume for Jenkins data at /var/jenkins\_home.

1. **Access Jenkins**: After starting the container, you can access Jenkins by opening a web browser and navigating to [http://localhost:8080](http://localhost:8080). You will be prompted to enter an initial administrator password, which you can find in the Jenkins logs by running the following command:
    

```plaintext
docker logs <container-id>
```

Replace &lt;container-id&gt; with the actual ID of the Jenkins container.

1. **Set up Jenkins**: Follow the on-screen instructions to set up Jenkins, including installing any necessary plugins and creating an administrator account.
    

That's it! You now have Jenkins running in a Docker container.

Once Jenkins is installed and configured, you can start creating jobs to automate your software development processes. Overall, installing Jenkins can be a straightforward process if you follow the instructions for your operating system and have the necessary prerequisites installed.