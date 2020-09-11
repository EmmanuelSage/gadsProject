# Getting Started with Compute Engine

## Objectives

In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.


## Task 1: Sign in to the Google Cloud Platform (GCP) Console

1. Use your credentials to sign in to the Google Cloud Platform .

2. Accept the terms.


## Task 2: Create a virtual machine using the command line

To Create a virtual machine we would run these command using the Command line.

1. we could first set the projectID using 

  ```shell
  gcloud config set project <PROJECTID>
  ```

2. Here we specify the optiona for the virtual machine, most of which could be left out so 
as to use the defaults. We set a tag of http so we can later set a firewall rule to allow http

   ```shell
   gcloud compute instances create my-vm-1 --machine-type 'n1-standard-1' --image-project 'debian-cloud' --image 'debian-9-stretch-v20190213' --subnet 'default' --tags http 
   ```

3. Targeting the tag of http we set a firewall rule to allow ingress traffic on port 80, which is the default.

  ```shell
   gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=http:80 --target-tags=http
   ```

## Task 3: Create a second virtual machine using the Command line

1. In this command we display a list of the zones in a region by listing the zones and then 
piping it to grep so as to filter by us-central1 region

   ```shell 
   gcloud compute zones list | grep us-central1 
   ```

2. We then choose a different zone than the first VM i.e us-central1-b


   ```shell
   gcloud config set compute/zone us-central1-b
   ```

3. After which we create the second Virtual Machine using.

   ```shell
   gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"
   ```

## Task 4: Connect between VM instances

1. First we `SHH` into my-vm-2 to test a ping to my-vm-1

    ```shell
      gcloud compute ssh my-vm-2 
      ```

2. we then use the `ping` command to confirm that my-vm-2 can reach my-vm-1 over the network

   ```shell
   ping -c 3 my-vm-1
   ```

3. Use the `ssh` command to open a command prompt on my-vm-1

   ```shell
   ssh my-vm-1
   ```

4. At the command prompt on `my-vm-1`, install the Nginx web server

   ```shell
   sudo apt-get install nginx-light -y
   ```

5. Use the `nano` text editor to add a custom message to the home page of the web server

   ```shell
   sudo nano /var/www/html/index.nginx-debian.html
   ```

6. Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace `YOUR_NAME` with your name

   ```
   Hi from YOUR_NAME
   ```

7. Press `Ctrl+O` and then press `Enter` to save your edited file, and then press `Ctrl+X` to exit the nano text editor.

8. Confirm that the web server is serving your new page. At the command prompt on `my-vm-1`, execute this command:

   ```shell
   curl http://localhost/
   ```

  - Result: The response will be the HTML source of the web server's home page, including your line of custom text

9. To exit the command prompt on `my-vm-1`, execute this command

  ```shell
   exit
   ```

10. To confirm that `my-vm-2` can reach the web server on `my-vm-1`, at the command prompt on `my-vm-2`, execute this command:

   ```sh
  curl http://my-vm-1/ 
  ```


- Result: The response will again be the HTML source of the web server's home page, including your line of custom text

11. Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text.

[Return to Readme](../README.md)