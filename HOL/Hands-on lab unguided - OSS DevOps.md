![](images/HeaderPic.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
OSS DevOps
</div>

<div class="MCWHeader2">
Hands-on lab unguided
</div>

<div class="MCWHeader3">
April 2018
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2018 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [OSS DevOps hands-on lab unguided](#oss-devops-hands-on-lab-unguided)
    - [Abstract and learning objectives](#abstract-and-learning-objectives)
    - [Overview](#overview)
    - [Solution architecture](#solution-architecture)
    - [Requirements](#requirements)
        - [Help References](#help-references)
    - [Exercise 1: Deploy the Web Application and Database to Azure](#exercise-1--deploy-the-web-application-and-database-to-azure)
        - [Task 1: Create the MySQL database](#task-1--create-the-mysql-database)
        - [Task 2: Restore the osTicket database to MySQL PaaS](#task-2--restore-the-osticket-database-to-mysql-paas)
        - [Task 3: Create the Web App](#task-3--create-the-web-app)
        - [Task 4: Configure the osTicket Web App](#task-4--configure-the-osticket-web-app)
        - [Task 5: Configure FTP deployment credentials](#task-5--configure-ftp-deployment-credentials)
        - [Task 6: Configure a staging slot](#task-6--configure-a-staging-slot)
        - [Summary](#summary)
    - [Exercise 2: Configure local Git repository](#exercise-2--configure-local-git-repository)
        - [Task 1: Clone a GitHub repository locally](#task-1--clone-a-github-repository-locally)
        - [Summary](#summary)
        - [](#)
    - [Exercise 3: Configure Git and Jenkins for continuous integration, delivery and deployment](#exercise-3--configure-git-and-jenkins-for-continuous-integration--delivery-and-deployment)
        - [Task 1: Deploy a Jenkins server in Azure](#task-1--deploy-a-jenkins-server-in-azure)
        - [Task 2: Post-Deployment configuration of the Jenkins server](#task-2--post-deployment-configuration-of-the-jenkins-server)
        - [Task 3: Configure Jenkins staging deployment](#task-3--configure-jenkins-staging-deployment)
        - [Task 4: Configure your GitHub repo to notify Jenkins of changes](#task-4--configure-your-github-repo-to-notify-jenkins-of-changes)
        - [Task 5: Check in a change to trigger Jenkins job](#task-5--check-in-a-change-to-trigger-jenkins-job)
        - [Task 6: Manually deploy to production](#task-6--manually-deploy-to-production)
        - [Summary](#summary)
    - [After the hands-on lab](#after-the-hands-on-lab)
        - [Task 1: Delete Resources](#task-1--delete-resources)

<!-- /TOC -->

# OSS DevOps hands-on lab unguided

## Abstract and learning objectives 

Migrate an online health food supplier from a hosted environment to Azure and fully embrace modern DevOps tools, investigate PaaS Services and leverage their existing knowledge of Jenkins integration with Azure.

Attendees will be better able to deploy complex OSS workloads into Azure PaaS using Azure App Services as well as the following tasks:

-   Deployment and integration of Azure Marketplace products from Partners such as Bitnami for Jenkins

-   Update Azure App Services using providers such as GitHub

## Overview

The scenario will challenge you to setup continuous integration and delivery of an application using open source tools such as Jenkins and GitHub along with automated deployments to Azure App Services. You will learn about continuous deployment and the benefits of staged publishing.

## Solution architecture

![Solution architecture to setup continuous integration and delivery of an application using open source tools such as Jenkins and GitHub with automated deployments to Azure App Services.](images/Hands-onlabunguided-OSSDevOpsimages/media/image2.png "Solution architecture diagram")

## Requirements

1.  An Azure Subscription

2.  A GitHub account

### Help References
|    |            |       
|----------|:-------------:|
| **Description** | **Links** |
| Jenkins Documentation | <https://jenkins.io/doc/> |
| GitHub Documentation | <https://help.github.com/> |
| Azure Web Apps Documentation | <https://azure.microsoft.com/en-us/services/app-service/web/> |
| Azure Database for MySQL | <https://docs.microsoft.com/en-us/azure/mysql/> |
| Azure Database for MySQL | <https://docs.microsoft.com/en-us/azure/mysql/howto-create-manage-server-portal/> |
| Azure Database for MySQL | <https://docs.microsoft.com/en-us/azure/mysql/howto-manage-firewall-using-portal/> |
| Connect Azure Web App to Azure Database for MySQL | <https://docs.microsoft.com/en-us/azure/mysql/howto-connect-webapp/> |
| App Service for Linux | <https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-intro/> |
| Azure CLI | <https://docs.microsoft.com/en-us/cli/azure/install-azure-cli/> |



## Exercise 1: Deploy the Web Application and Database to Azure

Duration: 60 minutes

In this exercise, you will deploy the web application and database to Azure using Azure App Service and Azure Database for MySQL. The first steps will be to build the MySQL DB and then import the data using MySQL Workbench. Then, you will create the Azure Web App and connect it to GitHub to download the app using a Docker Container with PHP 7.0.

### Task 1: Create the MySQL database

*Tasks to complete*

-   Deploy the Azure MySQL Database for the OS Ticket Application

*Exit criteria*

-   An instance of Azure Database for MySQL should be deployed

### Task 2: Restore the osTicket database to MySQL PaaS

*Tasks to complete*

-   Restore the osTicket database to the new MySQL database instance using the following script: <https://cloudworkshop.blob.core.windows.net/oss-devops/mysqlcluster.sql>

*Exit criteria*

-   The osTicket database should be deployed

### Task 3: Create the Web App

*Tasks to complete*

-   Create the Azure Web App (Linux) that will host the osTicket application

*Exit criteria*

-   An instance of Azure Web Apps (Linux) should be deployed

### Task 4: Configure the osTicket Web App

*Tasks to complete*

-   Fork the osTicket application from <https://github.com/opsgility/osTicket> and configure it to connect to the MySQL database.

*Exit criteria*

-   The application should be configured to reference your MySQL database

### Task 5: Configure FTP deployment credentials 

*Tasks to complete*

-   Configure the FTP credentials for the web app so that Jenkins can use them to deploy the application

*Exit criteria*

-   You should have the FTP credentials for the web app available for use

### Task 6: Configure a staging slot

*Tasks to complete*

-   Create a new deployment slot named Staging on the web app

*Exit criteria*

-   The new deployment slot should be created

### Summary

In this exercise, you used several Azure Platform as a Service (PaaS) components to configure a Web Application. The Web App will use Azure Storage as well as MySQL for data. You also configured a staging slot for the Web Application with duplicate settings. The actual deployment of the Web Application will happen in an upcoming exercise.

## Exercise 2: Configure local Git repository

Duration: 10 minutes

In this exercise, you will use the forked GitHub repository from the previous exercise and clone it locally so that you can configure your web app.

### Task 1: Clone a GitHub repository locally

*Tasks to complete*

-   Clone the GitHub repository you forked earlier to a local repository

*Exit criteria*

-   You should have a local repository with the osTicket source code cloned locally

### Summary

In this exercise, you cloned the previously forked GitHub repository locally, so you can configure your web app.

###  

## Exercise 3: Configure Git and Jenkins for continuous integration, delivery and deployment

Duration: 90 minutes

In this exercise, you will configure a Jenkins server in Azure and leverage it along with Git to setup continuous integration & delivery of your Web Application. You will be pulling source code from a GitHub repository and configuring Jenkins to build and deploy the code to your Staging slot before it is pushed to production (manually).

### Task 1: Deploy a Jenkins server in Azure

Jenkins is an open source continuous integration tool written in Java. It provides continuous integration services for software development. It is a server-based system running in a servlet container such as Apache Tomcat. In this exercise, you will deploy a Jenkins Server in Azure leveraging a prebuilt virtual machine image from the Azure marketplace.

*Tasks to complete*

-   Deploy a Jenkins server in an Azure Virtual Machine

*Exit criteria*

-   You should have a Jenkins server deployed in your Azure subscription

### Task 2: Post-Deployment configuration of the Jenkins server

*Tasks to complete*

-   Connect to your Jenkins deployment using SSH

-   Update Jenkins to the latest version

-   Configure Git for Jenkins

*Exit criteria*

-   You should have a connection to the Jenkins server and should have upgraded it to the latest version

-   Git should be configured on the Jenkins server

### Task 3: Configure Jenkins staging deployment

*Tasks to complete*

-   Configure Jenkins to deploy the osTicket application from your GitHub forked repository to the staging slot of your Azure Web App

*Exit criteria*

-   After this task, the osTicket application should be browsable from the staging slot of your Azure Web App

### Task 4: Configure your GitHub repo to notify Jenkins of changes

*Tasks to complete*

-   Configure Jenkins to use Web Hooks to be notified when changes occur in your GitHub repository

*Exit criteria*

-   After this task, the osTicket application should automatically deploy code changes checked into GitHub

### Task 5: Check in a change to trigger Jenkins job

*Tasks to complete*

-   Make a change to osTicket\\include\\client\\footer.inc.php file to add **Run on Azure App Services!** After **All rights reserved** on the page.

-   Commit and push your changes to the repository

*Exit criteria*

-   After this task, the **Run on Azure App Services!** text should be visible on the staging slot

### Task 6: Manually deploy to production

*Tasks to complete*

-   Swap the staging slot to production in your Azure Web App

*Exit criteria*

-   After this task, the application should load on the production URL

### Summary

In this exercise, you leveraged Azure, Jenkins and GitHub to setup continuous integration, delivery, and deployment for your web site. You built a scenario where your code changes were automatically pushed out to a staging slot after collecting assets from GitHub.

## After the hands-on lab 

Duration: 10 minutes

### Task 1: Delete Resources

1.  Now that the Hands-on lab is complete, go ahead and delete all the Resource Groups that were created for this lab. You will no longer need those resources and it will be beneficial to clean up your Azure Subscription.

You should follow all steps provided *after* attending the Hands-on lab.