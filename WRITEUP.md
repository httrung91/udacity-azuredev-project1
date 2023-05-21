# CMS APPLICATION DEPLOYENT ANALYSIS: AZURE VIRTUAL MACHINE VS AZURE APP SERVICE

## 1. Introduction
This document will compare and contrast the two popular solutions for deployment of web application on Azure Cloud for the CMS application deployment project. The first option is by using Azure Virtual Machine. The second option is to use the managed Azure App Service, also known as Azure Web App. By comparing the two methods, the reasoning for choosing one of the solution would also be explained at the end of the document

## 2. Deployment Process

This section only concerns about the process of how to deploy the app to the two compute services. The backend database adn storages, as well as the authentication process should be similar for both methods.

### 2.1 Virtual Machine

The steps for CMS Application Deployment can be summarized as below.
1. A virtual machine is created to host the the application.
2. After the machine is deployed, ssh connection to the virtual machine.
3. Install Python and python packages that are required by the CMS Flask application.
4. Install Nginx service for serving https request.
6. Setting the Environment variables that the application will use to reach the backend database, storage and Azure AD authentication service.
5. Configure Nginx service so that the HTTPS requests reach the CMS application.
6. Start the application.

After the above steps are completed, the CMS application can be access by requesting the public IP of the virtual machine in the browser.

### 2.2 Azure App Service (Web App)

The steps for CMS Application Deployment can be summarized as below.
1. Create a Azure App Service (Web App).
2. Configure the Environment Variables that the application will use to reach the backend database, storage and Azure AD authentication service.
3. Configure the connection to git repository (Git Hub) for automated deployment.
4. The App Service will automatically pull the source code from the git repository and start the deployment process.

After the App Service completes the deployment, the application can be reached from the browser by the provided URL.

## 3. COMPARISON

### 3.1 Deployment Workflow
From the deployment process in section (2), we can see that the solution using the Azure App Service is simpler than using the solution using Azure Virtual Machine. For the Azure App Service which is the managed service of Azure, the application developers are only required to setup the application configuration. There is no need to manage the underlying operating system and software packages or actual detail configuration of web server like Nginx. The process is simplified and quicker for the application to go live.

In addition, a simple automated deployment process can be integrated right a way by connecting the git repository to the App Service. The developers can make change to the code  and when a new version is published. the application is automatically deployed. This can be further expanded into a full CI/CD solution later. On the other hand, Virtual Machine solution requires further work and effort to setup automated deployment or CI/CD process.

While both services utilize the virtual machines for hosting application, the developers need to manage the Virtual Machines in Azure Virtual Machine solution. The instances of Azure App Service are managed by Azure platform. The only drawback here for App Service method compared to Virtual Machine method is that the developers do not have a completed control of their hosting environment. However, since the focus here is application development, this is not a significant concern.

### 3.2 Scalability 
Both Virtual Machine and App Service can be setup for scalabilty. In term of scaling up (vertical scaling), new virtual machine with more powerful configuration can be deployed, while the pricing tier of App Service can be increased to achieve more computation power. In term of scaling out (horizontal scaling), developers can use Scale Set for Azure Virtual Machine and Automatic Scaling for App Service to achieve scalability requirement.

### 3.3 Availability
Both Virtual Machine solution and App Service Solution can also deploy multipler instances to be highly available. Both methods can also be configured to deploy instances across availability zones of Azure Cloud. This can increase the availability and resiliency of the application. Also, both methods can also be integrated with other load balancing and cdn services.

### 3.4 Costs
In term of costs, an instance in a Azure App Service tier is more expansive than an instance of Azure Virtual Machine with a similar CPU and RAM configuration. Azure App Service is also not flexible in term of instance configuration, with each tier the instance configuration for CPU, RAM and disk storages are fixed. Virtual Machine solution offers a more flexible configuration between CPU, RAM and disk storages. On average, virtual machines are less expensive for production. Virtual machine solution can be significantly cheaper if the application grow and require to have high number of instances in the future. 

## 4. Solution Selection
For the CMS application of this project, using Azure App Service to deploy the application is selected. The reasons are the easy and quick deployment steps. Azure App Service can be integrated with git repository for automation. The application development can be focused without concering the underlying infrastructure. In addition, the first tier of App Service is free for testing the application.

## 5. App Changes Assessment
Azure App Service can be a more suitable solution for startup and small company that need to develop and deliver the application quickly. However, when the application size increase to have multiple instances, the cost of hosting the application could be increased significantly. Switching to the Virtual Machine solution would be suitable for reducing cost in comparison to App Service. 

Other reason to changing from App Service to Virtual Machine could be:
1. The application require hybrid setup with On-Premise resources: Virtual Machine would be more stuibale in this case.
2. Specific requirements in term of CPU, RAM and Disk storages: Virtual Machines are more flexible in this configuration requirement. 

