# cloud1

The process in how I created Cloud-1:

- Launch RDS Database with MySQL engine
   - containing:
      - Multi AZ Deployment (synchronously replicates data to standby instance)
      - VPC & Security Groups
      - Subnets
      - Endpoint
      - Add inbound rule for VPC Security Group
      
- Download Wordpress (https://wordpress.org/wordpress-4.9.5.tar.gz)

- Launch an Elastic Beanstalk environment (Load Balanced) using managed PHP Platform v7.0
     - Elastic Beanstalk is connected via the RDS database using environment properties
     - EC2 security groups are added to this as well
     - VPC and Subnets are added to the 'efs-create.config' which is for wordpress which is
       then uploaded to the EB instance
     - Once this is uploaded Wordpress will be installed.
     - Thereafter Access Restrictions will be removed by deleting the loadbalancer config file
       and then wordpress will need to be reuploaded to EB instance
     - Auto Scaling groups will be set to a minimum of 2 instances and max 4 so there are atleast 2 always running

- Route53
      - Hosted Zones are created via wordpress domain & record set created from domain ip

- S3 Bucket (Storage in the Cloud)
      - Bucket name matches wordpress site url

- IAM (Identity and Access Management Console)
      - create user and user group which will be used for CDN and 'W3 Total Cache'-wordpress plugin

- W3 Total Cache (wordpress plugin settings)
      - CDN Type: Origin Pull/Mirror Amazon Cloudfront
      - Access Key and Secret key credentials from IAM
      - Through W3 setup you create the Cloudfront Distrobution which setup on aws platform
      
      
# Cloud1 Schema     
<img width="824" alt="Screenshot 2020-05-21 at 17 05 49" src="https://user-images.githubusercontent.com/39004363/82573638-50b23280-9b86-11ea-90f6-c938ff832f61.png">

