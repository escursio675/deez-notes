#personal 


# Monitoring and Autoscaling
**CloudWatch**
CW is a metrics repository where AWS will store statistics and logs which can be retrieved by the user

**Autoscaling**
- Autoscaling prevents over and underprovisioning. This is done through EC2 autoscaling
- An autoscaling group defines, max, min and desired capacity
- A _Fleet_ is a group of EC2 instances running the application
- If any instances in the fleet fail a health check, they are automatically replaced

**Load Balancer**
- The Elastic Load Balancer is a fully managed service that automatically distributes traffic across instances among AZs
- The ELB has features of high availability, health checks, SSL termination and Monitoring

**Application Load Balancers**
- They distribute HTTP/S requests to different targets at layer 7 of the OSI model(Application Layer)

**Network Load Balancer**
It performs load balancing at layer 4(Transport Layer) and targets IPs, EC2 instances, containers etc

**Database Services**
Options are DB on EC2 AWS RDS. More control over databases require DB administration and OS level expertise. They provide low administrative burden,  high availability and durability, automated backups, push button scaling

**Aurora**
- It is a fully-managed db engine that provides various features and functionalities. It is significantly faster than MySQL and PostgreSQL.
- It is fully managed, highly secure, high availability, durability, performance and scalability and low cost

**DynamoDB**
- Also a fully managed db service that supports document and key-valued models with extreme horizontal provisioning.
- It is used for serverless web apps, microservices data store, mobile backends, ad tech, IoT

**Other Amazon db services**
1. Redshift - data warehouse with machine learning capabilities
2. DocumentDB - mongoDb compatible, works well with JSON data
3. Neptune - graph db
4. AWS Database Migration Service - quick and secure migration of data from other database services

# Deployment, DNS and CDN
**AWS CloudFormation**
- AWS CloudFormation allows us to create a collection of related AWS resources in an orderly fashion
- A template of the infrastructure can be created using JSON, YAML or gui

**Elastic Beanstalk**
- EB is used for deployment and it automatically manages Resource Provisioning, Load Balancing, Automatic Scaling and Monitoring
- It provides different application platforms, deployment options, health checks, monitoring, scaling and update notifications along with compliance and customization

**Direct Connect**
- creates a dedicated private network between on-premise data center and AWS cloud
- It reduces bandwidth cost, provides consistent network performance and private connection to VPC with easy scalability

**Route53**
- a DNS service in AWS
- it routes traffic, health checks, registration of domain names

**Elastic File System**
- shared file system storage for linux workloads
- It provides dynamic elasticity, scalable performance, shared file storage, cost effective and fully managed

**Lambda**
- it is a serverless utility for running applications
- paid only for the duration the code runs

**Simple Notification Service**
SNS is a messaging service for distributed applications

**CloudFront**
- CND service that implements caching
- If provides faster performance, security against network and application layer attacks, programmable and cost effective

**ElasticCache**
- in-memory database service in the cloud
- it provides extreme performance that is scalable

## Security and Compliance
Under the Shared Responsibility Model, "Security of the Cloud" refers to the security responsibilities of AWS(protecting infrastructure, regions, AZs, edge locations) whereas "Security in the Cloud" of the user/customer(content uploaded, country in which it is available, who has access etc).

Some security products are: AWS Artifact, Certificate Manager, Cloud Directory, CloudHSM(Hardware Security Module), Cognito, Directory Service, Firewall Manager, Guard Duty, IAM(Identity Access Management), Inspector, KMS(Key Management Service), Macie, Organizations, Shield(DDoS protection), Secrets Manager, Single Sign-On(SSO), WAF(Web Application Firewall)

### Authentication and Authorizaion
**IAM**
- Create users, groups and roles for access and authentication
- The root user is the one that creates the account. It is common practice to delete root user access keys and create a admin IAM user

**Inspector**
- It assesses the application for vulnerabilities, exposure and deviations from best practices
- It contains a large set of rules to perform the above

**Shield**
- Creates a number of rules to mitigate DDoS but allowing us to define a set of rules
- Shield Standard has no cost and quick detection
- Shield Advanced provides advanced detection with visibility and attack notifications along with specialized support

## Cloud Architecture and Design Principles
The AWS Well Architected Framework has six design principles-
1. Operational Excellence
2. Security
3. Reliability
4. Performance Efficiency
5. Cost Optimization
6. Sustainability

## Pricing and Application Control
- Payment options are All(AURI), Partial(AURI) and No upfront(NURI) payments
- AURI provides the largest discount
- The more the volume, more is the discount
- Factors that affect cost are compute, storage and data transfer considerations
- Pricing also varies per service used
- S3 storage pricing depends on amount used, region, storage class, number and type of requests, amount of data transferred out of region
- The Trusted Advisor tool can be used to provide guidance in reducing cost, increasing performance and security
- AWS Support provides further help. It includes plans- Basic(free), Developer, Business and Enterprise