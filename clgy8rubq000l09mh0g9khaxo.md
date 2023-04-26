---
title: "Setup of KUBERNETES CLUSTER on AWS"
seoTitle: "Setup of KUBERNETES CLUSTER on AWS"
seoDescription: "Setup of KUBERNETES CLUSTER on AWS"
datePublished: Wed Apr 26 2023 22:02:29 GMT+0000 (Coordinated Universal Time)
cuid: clgy8rubq000l09mh0g9khaxo
slug: setup-of-kubernetes-cluster-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682546429514/54b15f41-4f08-4fd0-a434-43365561e9b9.png
tags: docker, kubernetes, devops, kubeadm

---

For the Kubernetes setup, we need two EC2 instances.

1. Master Node
    
2. Worker Node
    

To create a master node and worker node of Kubernetes in AWS EC2, follow these general steps:

1. **Launch an EC2 instance:** First, you need to launch an EC2 instance with your preferred operating system. You can choose from a variety of options such as Ubuntu, CentOS, or Amazon Linux.
    
2. **Install Docker:** Once your instance is up and running, you need to install Docker, which is a prerequisite for Kubernetes. Here's how you can install Docker on Ubuntu:
    
    ```yaml
    sudo apt-get update 
    
    sudo apt-get install docker.io -y 
    ```
    
3. **Install Kubernetes:** Now you can install Kubernetes using the official installation script. Here's how you can do it:
    
    ```yaml
    sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2 
    
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    
    echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    
    sudo apt-get update 
    
    sudo apt-get install -y kubelet kubeadm kubectl 
    ```
    
4. **Initialize the cluster:** After installing Kubernetes, you need to initialize the cluster using the kubeadm init command. Here's an example command:  
    
    ```yaml
    sudo kubeadm init --pod-network-cidr=192.168.0.0/16 
    
    
    This command initializes the cluster and sets the pod network CIDR to 192.168.0.0/16.
    ```
    
5. **Configure kubectl:** Once the cluster is initialized, you need to configure kubectl, which is the command-line tool used to interact with Kubernetes. Here's how you can do it:
    
    ```yaml
    mkdir -p $HOME/.kube 
    
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config               
    sudo chown $(id -u):$(id -g) $HOME/.kube/config        
    ```
    
6. **Install a Pod network:** Finally, you need to install a pod network to enable communication between pods in the cluster. There are several options available, but one of the most popular choices is Flannel. Here's how you can install Flannel:
    
    ```yaml
    kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml 
    ```
    
7. **Set up EC2 instances for the worker nodes:** Launch EC2 instances using the same security group as the master node.
    
8. **Join the worker nodes to the cluster:**
    
    * Log in to each worker node using SSH.
        
    * Run the `kubeadm join` command saved from the master node initialization step.
        
    * Verify that the worker nodes have joined the cluster using the `kubectl get nodes` command on the master node.
        

After completing these steps, you should have a Kubernetes cluster running on AWS EC2 with a master node and one or more worker nodes. Note that these are general steps and your specific setup may require additional steps or configuration. It's also important to follow security best practices when setting up a Kubernetes cluster on AWS EC2.