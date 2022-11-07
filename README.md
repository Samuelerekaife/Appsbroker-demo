
# Appsbroker Team Purple

## Task 1 - Using Google Cloud  

### Create and Configure a Web Server on Google Cloud Platform

A brief description of the exact steps to follow inorder to create and configure a web server on Google Cloud Platform.

#### Requirements

- Use Google Cloud Console
- It should have a Linux distribution OS with Apache
- How can the web server be scalable to meet a "High Availabilty" requirement?
- Follow "Google Cloud best practice" and should be "Secure by design"

#### Action Plan

- Create a Linux virtual machine (VM) instance in Compute Engine using the Google Cloud console.
- Connect to the VM instance via SSH
- Install and configure Apache web server inside this VM
- Deploy web application inside the Apache web server
- Access the web application from browser

#### Before you begin

1. If you're new to Google Cloud, create an account to evaluate how Google Cloud products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.
2. In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
3. Make sure that billing is enabled for your Cloud project.
4. Enable the Compute Engine API.

#### Execution Steps

1. Create a Linux VM instance in Compute Engine 
- In the Google Cloud console navigation menu, click Compute Engine > VM instances
- Click Create instance
- In the Name field, enter an instance name. Here I will be naming this instance appsbroker-team-purple
- In the region section, select europe-west2 (London) as region and europe-west2-c as zone.
- In the CPU section, select E2
- In the Boot disk section under public images, select SSD persistent disk while in the OS section, select Linux
- For Identity and API access, select Compute Engine default service account and allow default access to API
- In the Firewall section, select  the Allow HTTP traffic checkbox to open port tcp:80 for traffic
- In the Networking section, assign ephemeral public ip address which means a temporary ip address will be allocated to the VM everytime the VM starts
- Click Create.
Your new instance appears on the VM instances page. When a green checkmark appears, you can connect to the instance

2. Connect to the VM instance via SSH
- In the Google Cloud console, go to the VM instances page
- On the VM instances page, look in the Name column to find the VM instance you created
- In the list of virtual machine instances, click SSH in the row of the instance that you want to connect to
- In the Connect column of the VM instance, click SSH
A new command prompt opens and shows that you are connected to your VM terminal

3. Install and configure Apache web server inside this 
- In the Google Cloud console, go to the VM Instances page
- To connect to the Linux VM you just created, click SSH in the row of the VM
- To update the available packages and install the apache2 package, run the following commands
sudo apt update

sudo apt -y install apache2

- After installing Apache, the operating system automatically starts the Apache server. Verify that Apache is running using the command below
sudo systemctl status apache2

-Overwrite the Apache web server default web page by using the command below

echo '<!doctype html><html><body><h1>HelloTeamPurple!</h1></body></html>' | sudo tee /var/www/html/index.html

4. Access the web application from browser
- Test that your VM is serving traffic on its external IP
- In the Google Cloud console, go to the VM Instances page
- Copy the external IP for your VM under the External IP column
- In a browser, navigate to http://[EXTERNAL_IP]
- You should now see the "Hello Team Purple!" page.

## How can the web server be scalable to meet a "High Availabilty" requirement?

From my research, inorder for a web server to meet high availability, it needs to scale globally. This can be done with regional Compute Engine managed instance groups that automatically scale to meet capacity needs.

### Objectives

- Deploy multiple regional Compute Engine managed instance groups with autoscaling enabled
- Create a cross-region load balancer
- Generate test traffic from different regions across the globe
- Use the Google Cloud console to visualize how the load balancer routes requests and how the instance groups autoscale to meet demand

### Application architecture

The application includes the following Compute Engine components:

1. Instance template: A template used to create each instance in the instance groups.
2. Instance groups: Multiple instance groups that autoscale based on incoming traffic.
3. Load balancer: An HTTP load balancer that distributes traffic among the instance groups.
4. Instances: Multiple testing instances to generate test traffic from different parts of the globe.

#### Execution Steps

1. Set up the web service to create the instance group.
2. Configure the load balancer. The load balancer will distribute client requests among your multiple backends.
3. Host and path rules and configure the frontend of the load balancer.
- Best Practice: Create a secure firewall to allow only internal traffic from the load balancer and the health check. Then delete the original firewall that allowed any HTTP request. This prevents individual instances from being accessible by outside clients.
4. Verify that autoscaling and load balancing works.
5. Monitor load balancing and autoscaling.
6. Generate test traffic somewhere else.
7. Monitor load balancing and autoscaling.

### Google Cloud Best Practices and Secure by design
Clean Up: To avoid incurring charges to your Google Cloud account for the resources used, follow these steps to delete the VM

1. In the Google Cloud console navigation menu, click Compute Engine > VM instances.
2. Click More actions in the same row as the instance you want to delete.
3. At the top of the instance's details page, click Delete and confirm.


## Task 2


