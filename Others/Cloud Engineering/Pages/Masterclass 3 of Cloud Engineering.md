#personal 
# NIST Model

- 5 essential characteristics, 3 service models, 4 deployment models
- on demand self-service, broad network access, resource pooling, rapid elasticity, measured service

# Cloud Cube Model
- internal/external, proprietary/open, parameterised/deparameterised, insourced/ousourced


# Cloud Architecture
- physical, infra, platform, application layers

# Regions and Availability Zones
- region is a geographical boundary
- a region has a min of 3 AZs


# Shared Responsibility Model
Whatever is in the cloud is handled by the user and whatever is off the cloud is handled by the cloud provider

# Shared Tenancy Model
A host may contain software running from various organizations. A dedicated host allows us to run software exclusively from one organization on the same host.

# Composability
Replace individual components of a web app, eg, static assets(S3), auth(cognito)

# Trade-offs
Need fast deployment + small team?         → Elastic Beanstalk  
Need full control + compliance?            → EC2 + ASG + ALB  
Running containers?                        → ECS Fargate  
Already on Kubernetes?                     → EKS
