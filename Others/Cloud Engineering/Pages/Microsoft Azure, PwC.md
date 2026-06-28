#personal 

## CapEx and OpEx
CapEx refers to the huge upfront payment made on physical infrastructure. These depreciate over time.

OpEx refers to the pay-as-you operational costs.

## Azure Container Instance(ACI)
It is a lightweight container for running applications without an OS. Applications from different organizations are isolated through hypervisor layers

## Azure Kubernetes Service(AKS)
A number of kubernetes commands are used to manage the different containers

## Azure App Services
A fully manged platform to build web based applications that scale easily on both windows and linux environments with additional features like security

## Azure Storage Services
These include 
1. **Azure Blob Storage** - object storage for storing unstructured data for backup, archiving and recovery. Access tiers include Hot, Cold and Archive Access Tiers
2. **Azure Files Storage**
3. **Azure Queues Storage** - used to store numerous messages accessed using authenticated HTTP/S requests, max size of a message being 64KB. The default time to live of a message is 7 days
4. **Azure Disk Storage** - block level _virtualized_ storage used with Azure Virtual Machines. They can be standard and premium SSDs and standard HDDs
5. **Azure Tables Storage** - non-relational structured data storage with key/attribute store in a schema less design. Accessing the data is fast and cost effective with lower cost than traditional SQL. Data can be queried faster using clustered index 

There can be unlimited number of **Containers** in a storage account and each container can have an unlimited number of blobs. The container name must be a valid dns name, between 3 and 63 characters and start with a letter or number and can have only lowercase letters, numbers and hyphen. Two or more consecutive hyphens are not allowed.

## Azure Network Services
Virtual Networks are the fundamental building blocks of private networks and allow resources to securely communicate with each other. Incoming and outbound traffic are managed through a public IP or load balancer.

Communications of on-premises resource are through **Point-to-site VPN**, **Site-to-site VPN** and **Express Route**.

**Azure Vritual Network Peering** is used to connect multiple virtual networks through Microsoft's private network.

**Global Network Peering** is used to connect several Azure regions with low latency and high bandwidth. This is done through Microsoft's backbone network

## Data Services
**Azure ComosoDB** is a globally distributed multi-model db service. It is a fully managed NoSQL database

**Azure SQL Database** is a an RDBMS with the Microsoft SQL Server Engine used to build data driven applications. It also supports non-relational structures like graphs, JSON, XML etc.

## Identity Services
As opposed to **Authentication** which involves identification of users through access credentials, **Authorization** refers to the level of access of an authenticated person as well can what data can be accessed and what can be done with that data.

Azure uses **Azure Active Directory(ADD)** as its identity and access management service. It includes conditional access, granulated access management or Role Based Access-Control(RBAC), resource locks, tags and Azure Policy.

**Azure Blueprints** helps organizations set up new environments rapidly.

## Azure Pricing
Factors that affect cost are - 
1. Resource Types - incoming and outgoing traffic, size etc
2. Services
3. Location
4. Bandwidth
5. Reserved Instance
6. Hybrid Benefits

The **Pricing Calculator** is used along with the **Total Cost of Ownership(TCO) Calculator**.

Detailed information regarding the services can be found in the **Service Level Agreements(SLAs)**. Free services do not have SLAs.

## Azure Solutions
**Azure IoT** is a globally managed IoT SAAS solution for connecting, monitoring and managing IoT assets easily.

### Big Data Services
1. **Azure Synapse Analytics** - data warehousing and big data analytics
2. **HDinsight** - fully-managed, open-source analytics service for organizations
3. **Databricks** - Apache-Sparks based analytics service

### AI and Machine Learning
1. **Azure Machine Learning** - develop, train and install machine learning models
2. **Cognitive Services** - understand the users' needs
3. **Bot Service** - enterprise-grade bots

### Serverless Computing
1. **Azure Functions** - event based code runs without an underlying infrastructure
2. **Azure Logic Apps** - automate tasks and processes into integrated apps

### DevOps
1. **Azure DevOps** - development collaboration tools including pipelines and automated cloud-based load testing
2. **DevTest Labs** - quick environment creation with minimization of costs
3. **GitHub**
4. **GitHub Actions for Azure** - automated software workflows to build, test and deploy from GitHub

### Management Tools
1. **Azure Advisor** - optimize installations and recommendations based on best practices
2. **Azure Monitor** - logs and alerts to maximize usability and performance of resources
3. **Service Health Alerts** - service incidents and intended maintenance to reduce downtime
4. **Azure Resource Manager(ARM)** - templates to deploy app resources and organize them as well as control access to resources