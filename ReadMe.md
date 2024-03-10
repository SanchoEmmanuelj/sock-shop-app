This body of work is my submission for the end of course capstone project.

Project Overview:

Objective: We aim to deploy a microservices-based application, specifically the Socks Shop, using a modern approach that emphasizes automation and efficiency. The goal is to use Infrastructure as Code (IaaC) for rapid and reliable deployment on Kubernetes.

For my submission we are going to be deploying the sock shop application with Kubernetes using Terraform

- we are going to be deploying 10 services — carts, catalogue, frontend, orders, payment, queue-master, rabbitmq, session-db, shipping, and user

- These 10 services are what makes up the sock-shop microservice.

Setup Details Explained:
What You'll Do: Your main task is to set up the Socks Shop application, a demonstration of a microservices architecture, available on GitHub. You'll be using tools and technologies that automate the setup process, ensuring that the application can be deployed quickly and consistently.

Resources:
Socks Shop Microservices Demo: GitHub Repository
Detailed Implementation Guide: GitHub Repository
Task Instructions:
Use Infrastructure as Code: Automate the deployment process. This means all the steps to get the application running on Kubernetes should be scripted and easily executable.
Focus on Clarity and Maintenance: Your deployment scripts and configurations should be easy to understand and maintain. Think of someone else (or yourself in the future) needing to update or replicate your setup.


Security and HTTPS: Make sure the application is accessible over HTTPS by using Let’s Encrypt for certificates. Consider implementing network security measures and use Ansible Vault for handling sensitive information securely.

Project Goals Summarized:

This project is about deploying a microservices-based application using automated tools to ensure quick, reliable, and secure deployment on Kubernetes. By focusing on Infrastructure as Code, you'll create a reproducible and maintainable deployment process that leverages modern DevOps practices and tools.

prerequisite:

- An Ubuntu machine
- Terraform installed
- Kubectl installed
- AWS CLI installed
- Helm installed 
- Jenkins instaled listening on port 8080

This project is made of 5 sections 

- EKS Directory
- Kubernetes Directory
- Jenkinsfile cluster
- Installer.sh
- Jenkinsfile

The Micro-service files in the micro-service directory include:

CARTS.TF:
this terraform-Kubernetes script deploys the carts application into the cluster.Create kubernetes deployment for cartm The carts application is going to be running on port 80 and Mongo DB as database.

CATALOGUE.TF:
just like the carts section, we are going to also be deploying the catalogue section of the sock-shop microservice running on port 80 and MySQL DB for database.

FRONTEND.TF
this will be the front page of the sock-shop application. it is going to also be deployed in the sock-shop namespace with 1 replica. The frontend service doesn’t have a database. it also runs on port 80.

MICRO-PROVIDER.TF
Here we create a providers file for the sock shop microservice 
creating a new namespace for it and we will be naming it sock-shop
We specify the location of the Kube config file for the providers listed.

ORDERS.TF
this is the service where customers can make orders.

PAYMENTS.TF
the payment service just like every other service will be deployed in the sock-shop namespace. with 1 replica.The payment service will be running on port 80

QUEUE-MASTER.TF
the file queue master runs on a port 80 with a CPU limit of 300m and memory limit of 500Mi,

RABBITMQ.TF
the RabbitMQ is for the order queue. and it has an exporter which runs on the port 9090.

SESSION-DB.TF
the session db is a Redis container that is used to store data and running on port 6379

SHIPPING.TF
the shipping service is where shipping is made in the sock shop microservice. it has its own image which we will be pulling from docker runs on port 80

USER
the user service is where users are created.The database used here is mongo db



On this project i included a bashscript (installer.sh) that installs all the dependensies to equipe the Ubuntu machine with all its dependencies.

The Process:

Create an instance on AWS or a Droplet on digital Ocean. i personally used an AWS t2 medium ubuntu instance.

Clone this repo into the instance or droplet you created by running the git clone command 

once you have all the files in this project copied from git to the instance you can then make the installer.sh bash scrip executable by running the (chmod +x installer.sh).

Run the scrip ./installer.sh once it runs succesfully then we are good to go.

Copy the Public IP Address of the instance and open jenkins on your through port 8080

Register the user on jenkins 

create pipeline for the EKS AND Sock-shop

Then Build 
![sock-shop](<Screenshot 2024-03-08 at 23.43.32.png>)


and 

after the build is done ensure to transfer aws nameserves to you domain provider

 ![dns](<Screenshot 2024-03-10 at 13.14.54.png>)

When we are all done we can nor open the sock-shop on our web brower at sock-shop.globalmerchantsmart.org and grafana.globalmerchantsmart.org

![sock-shop](<Screenshot 2024-03-08 at 23.36.28.png>)

and 

![grafana](<Screenshot 2024-03-08 at 23.36.39.png>)


and using the login

user: admin
pass: prom-operator


![Alt text](<Screenshot 2024-03-08 at 23.39.32.png>)



