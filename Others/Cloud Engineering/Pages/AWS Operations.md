#personal 

# Creating an S3 bucket

A normal flow is to:
1. Create a bucket
2. Create a folder within that bucket
3. Upload a file(as an object) within that folder

- The bucket name should be unique globally
- Region must be selected to provide the best response/least latency

# Hosting a static website

1. Login to AWS Management Console
2. Select S3
3. Create a bucket
4. Select the bucket and go to the Permissions tab
5. Disable the "Block all public access" setting and save
6. Head to Properties tab
7. Edit "Static Website Hosting" option and enable
	 - Enter 'index.html' and 'error.html' documents in the fields
	 - Save changes
8. The websit url can be found under the same "Static Website Hosting" option
9. Under the bucket, click on the "Upload" button, "Add Files" and upload the static html files
10. Under Permissions tab, enable ACLs
11. Under Objects tab, select the files, click on Actions and "Make Public"
12. The website can now be access from the previous link

# Amazon Virtual Private Cloud
The following highlights creating an Amazon VPC with two subnets- one public for hosting resources and other private for hosting business critial databases

1. In the AWS Management Console, select VPC
2. Under "Your VPC" click "Create VPC"
	 - Provide a name and the CIDR range as 10.0.0.0/16 then create
3. Under "Internet Gateway" click Create
	- Provide a name and create
4. Click on Actions-> Attach to VPC -> select your VPC and click attach
5. Under "Subnets" 
	 - create subnet 
	 - select your VPC
	 - specify name of subnet
	 - select Availability zone as ap-south-1a for Mumbai
	 - specify CIDR range as 10.0.1.0/24
	 - Create
6. To create private subnet, go to "Subnets"
	 - select your VPC
	 - assign subnet same 
	 - select same availability zone
	 - set CIDR range to 10.0.2.0/24
	 - create
7. To create a route table, under "Route Table"
	 - specify name
	 - specify VPC
	 - create
	 - Click "edit route"
	 - "Add route"
	 - set destination to 0.0.0.0/0
	 - set Target to Internet Gateway
	 - save
8. Under "Subnet Association" tab
	 - edit subnet association
	 - select the public subnet
	 - save

# Creating an EC2 instance and deploying a Web Application

1. In the AWS Management Console, select EC2
2. From "Security Groups" 
	 - create
	 - set name
	 - set description
	 - select vpc
	 - add inbound rule
		 - type = HTTP
		 - source = anywhere
		 - create
3. From "Instances", launch instance
	- choose amazon instance 2 Linux AMI
	- type = t2 micro and Next
	- number of instances = 1
	- select the VPC
	- enable auto-assign Public IP
	- install required packages in 'user data' at the bottom
	- next
	- size should be 8GB
	- add tags
	- next
	- select the previously created security group
	- review and launch
	- "Proceed without key-pair" and launch
4. View instance
5. Select the web server
	- copy the public IP under the Details tab
	- Browse the site at the IP address