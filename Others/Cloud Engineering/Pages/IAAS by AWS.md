#personal 

- Amazon S3 implements object level storage, ie, changing a file requires modification of the entire file.
- S3 stores data as objects in resources called buckets.
- By default, all S3 resources are private access control. The owner can grant acess to others by writing access policies. Policies can be resource based or user based policies implemented by JSON.
## Bucket Properties
- Versioning enabled buckets can store multiple versions of the same object in buckets.
- Other services include server access logging, tags, event notificatins, encryption, static website hosting, media hosting etc.
- Storage classes include standard(default), S3 Intelligence Tiering, infrequent access, One Zone infrequent access, Glacier and Deep Archive.
# Virtual Private Cloud(VPC)
- Service that lets users define logically isolated virtual network to launch AWS resources.
- Amazon VPC lets users create specific CIDR IP addresses for resources and create access rules for inbound and oubound traffic.
- VPC supports subnetting with the first 4 and last IP address reserved by AWS.

# Amazon Elastic Compute Cloud(EC2)
- Provides compute capacity in cloud
- Supports application, game, web servers etc
- Instance types have names of the form c5.large where c->family name, 5->generation number, large->instance size

# Amazon Machine Images(AMI)
- Master Images required for creation of EC2 images in AWS environment.
- They consist of root volumne template, launch permissions and block device mapping.

