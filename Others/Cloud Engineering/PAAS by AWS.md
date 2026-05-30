#personal 

# PAAS
PAAS provides a framework for deploying applications without concerning with the underlying hardware/infrastructure.

Disadvantage of using PAAS include vendor dependency, risk of lock-in, compatibility, security-risks.

Type:
- PAAS tied to SAAS product
- PAAS tied to Operating Environment
- Open-cloud PAAS

# Beanstalk
AWS Elastic Beanstalk allows for quick deployment without hardware provisioning. It automatically handles load balancing, resources provisioning, auto scaling and monitoring. It makes deployment simple and fast.

Beanstalk is compatible with languages like Go, Javascript, Python, Ruby etc.

## Deployment Options
- All at once
- Rolling
- Rolling with additional batch
- Immutable

# Deploying using Beanstalk
1. Choose "Elastic Beanstalk" from AWS Management Console
2. Under "Applications" tabs, create a new application
3. Set a name and create
4. Create new environment
	- select web server environment
	- set domain name
	- select a Platform, branch and version
	- create with a sample application
5. Access the environment by the URL under "All Environments" in the Environments tab.

# Deploying a Custom Application
1. Create Application
	-  set name
	- select platform, branch and version
2. Select "Upload your Code"
3. Select local file and upload
4. Create Application
5. Access the environment by the URL under "All Environments" in the Environments tab.
6. Under applications select the application and choose delete option under Actions to delete the application.