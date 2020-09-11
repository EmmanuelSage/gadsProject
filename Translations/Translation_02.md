# Google Cloud Fundamentals Getting Started with GKE

## Objectives:
In this lab, you will learn how to perform the following tasks:

 - Provision a Kubernetes cluster using Kubernetes Engine.

 - Deploy and manage Docker containers using kubectl.


## Task 1: Sign in to the Google Cloud Platform (GCP) Console

1. Use your credentials to sign in to the Google Cloud Platform .

2. Accept the terms.

## Task 2: Confirm that needed APIs are enabled

1. you can check for enabled services using 

      ```sh
      gcloud services list --available
      ```
  
2. if the below are not in the list of enabled APIs
      - Kubernetes Engine API
      - Container Registry API

3. If they are not in the list of enabled APIs enable them using 
      ```sh
      gcloud services enable container.googleapis.com containerregistry.googleapis.com
      ```

## Task 3: Start a Kubernetes Engine cluster

  1. Set your zone in an environmental variable
      ```sh
      export MY_ZONE=us-central1-a
      ```
  2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
      ```sh
      gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
      ```
  3. After the cluster is created, check your installed version of Kubernetes using the `kubectl version` command:
      ```sh
      kubectl version
      ```

## Task 4: Run and deploy a container

1. From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)
      ```sh
      kubectl create deploy nginx --image=nginx:1.17.10
      ```
2. View the pod running the nginx container:
      ```sh
      kubectl get pods
      ```
3. Expose the nginx container to the Internet:
      ```sh
      kubectl expose deployment nginx --port 80 --type LoadBalancer
      ```
4. View the new service:
      ```sh
      kubectl get services
      ```
5. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

6. Scale up the number of pods running on your service:
      ```sh
      kubectl scale deployment nginx --replicas 3
      ```
7. Confirm that Kubernetes has updated the number of pods:
      ```sh
      kubectl get pods
      ```
8. Confirm that your external IP address has not changed:
      ```sh
      kubectl get services
      ```   

[Return to Readme](../README.md)