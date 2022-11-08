![Logo](https://lh3.googleusercontent.com/lhmag1ZJ11TNS2phffnu7Ly4B07kYqHyPaoHt-LSbC607HJeAeRhot6kT5h3Hjnk=h100)

# Appsbroker Team Purple

## Task 1 - Using Google Cloud Console 

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

echo '<!doctype html><html><body><h1>Hello Team Purple!</h1></body></html>' | sudo tee /var/www/html/index.html

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

## Google Cloud Best Practices and Secure by design
Clean Up: To avoid incurring charges to your Google Cloud account for the resources used, follow these steps to delete the VM

1. In the Google Cloud console navigation menu, click Compute Engine > VM instances.
2. Click More actions in the same row as the instance you want to delete.
3. At the top of the instance's details page, click Delete and confirm.


## Task 2 - Design Spike

### Investigate 3 different ways of hosting a static content website on Google Cloud using a Google Cloud service other than Compute Engine

A brief documentation to show 3 ways of hosting a static content website on Google Cloud apart from using Compute Engine.

#### Requirements
- What is a static website
- Research on other ways in hosting a static content website apart from using compute Engine
- Preferred method and reasons

#### Action Plan

#### What is a static website?
A static content website simply means that the content you serve does not change in response to requests. Static websites are a good option for sites like blogs — where the page rarely changes after it has been published, or where there isn’t any dynamically-generated content. Static web pages can contain client-side technologies such as HTML, CSS, and JavaScript. They cannot contain dynamic content such as server-side scripts, like PHP.

#### 3 other ways in hosting a static website in Google Cloud
The 3 other ways of hosting a static website in Google Cloud include the following

1. Google App Engine.
2. Cloud Storage
3. Firebase hosting

#### Google App Engine
You can use Google App Engine to host a static website. Static web pages can contain client-side technologies such as HTML, CSS, and JavaScript. Hosting your static site on App Engine can cost less than using a traditional hosting provider, as App Engine provides a free tier.

Sites hosted on App Engine are hosted on the REGION_ID.r.appspot.com subdomain, such as [my-project-id].uc.r.appspot.com. After you deploy your site, you can map your own domain name to your App Engine-hosted website.

Before you can host your website on Google App Engine: Create a new Google Cloud console project or retrieve the project ID of an existing project to use and then initialize the Google Cloud CLI.


#### Cloud Storage

To host a static site in Cloud Storage, you need to create a Cloud Storage bucket, upload the content, and test your new site. You can serve your data directly from storage.googleapis.com, or you can verify that you own your domain and use your domain name. 

If you have a web app that needs to serve static content or user-uploaded static media, using Cloud Storage can be a cost-effective and efficient way to host and serve this content, while reducing the amount of dynamic requests to your web app.

Additionally, Cloud Storage can directly accept user-submitted content. This feature lets users upload large media files directly and securely without proxying through your servers.

#### Firebase Hosting

Firebase Hosting provides fast and secure static hosting for your web app. With Firebase Hosting, you can deploy web apps and static content to a global content-delivery network (CDN) by using a single command.

Firebase production-grade hosting is backed by a global content delivery network (CDN). Hosting serves your content over SSL, by default, and can be used with your own custom domain or on your project's subdomains at no cost on web.app and firebaseapp.com.

#### Preferred method and reasons

Each of these methods can be used to successfully host a static website in Google Cloud depending on the given requirements. All the services have their advantages and disadvantages over others.

However, on a personal preference, at the moment I would use Firebase hosting for my static website because of the following reasons 

1. Firebase Hosting offers lightweight configuration options even if you are not too familiar with Google Cloud services comapared to the other two options.
2. Firebase hosting is more cost effective and secure as it has a free tier plan where you connect your own domain name to Firebase Hosting and also provides an automatic zero configuration SSL certificate for your domain so all your content is served securely.
3. Firebase hosting has end-to-end HTTPS serving compared to Cloud Storage which doesn't support end-to-end HTTPS for custom domains.
4. Firebase hosting offers rapid deployment where you can use the Firebase CLI to get your app up and running in seconds with a one-click rollback feature to undo mistakes.


## References

https://cloud.google.com/security/best-practices

https://cloud.google.com/compute/docs/create-linux-vm-instance

https://cloud.google.com/compute/docs/tutorials/basic-webserver-apache

https://cloud.google.com/storage/docs/hosting-static-website

https://cloud.google.com/compute/docs/tutorials/high-availability-load-balancing

https://cloud.google.com/sql/docs/mysql/high-availability

https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes

https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

https://success.outsystems.com/Documentation/11/Setup_and_maintain_your_OutSystems_infrastructure/Setting_Up_OutSystems/Possible_setups_for_an_OutSystems_infrastructure/High_availability_and_scalability_strategies

https://cloud.google.com/compute/docs/tutorials/globally-autoscaling-a-web-service-on-compute-engine#console

https://cloud.google.com/architecture/web-serving-overview#static-site

https://firebase.google.com/docs/hosting/quickstart

https://cloud.google.com/load-balancing/docs/https/ext-load-balancer-backend-buckets

https://www.howtogeek.com/devops/how-to-host-a-high-performance-static-website-from-a-gcp-cloud-storage-bucket/

https://console.cloud.google.com/marketplace/details/google-cloud-platform/firebase-hosting?project=divine-turbine-367720

https://medium.com/google-cloud/hosting-a-static-website-on-google-cloud-using-google-cloud-storage-ddebcdcc8d5b

https://cloud.google.com/appengine/docs/legacy/standard/python/getting-started/hosting-a-static-website

https://www.websitebuilderinsider.com/what-are-the-advantages-of-hosting-static-website-on-google-cloud-storage/#:~:text=Security%3A%20Static%20websites%20are%20typically,or%20on%20a%20shared%20server.

https://www.fizerkhan.com/blog/posts/free-static-page-hosting-on-google-app-engine-in-a-5-minutes


