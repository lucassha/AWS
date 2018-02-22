### Basic Terminology

<hr>

### Cloud Computing

**Elastic Book Store (EBS)** - provides persistent block level storage volumes for use with EC2 instances in the AWS Cloud. Each EBS volume is automatically replicated within its Availability Zone to protect you from component failure

**Relational Database Service (RDS)** - web service that makes it easy to set up, operate, and scale a relational database in the cloud. Offers access to many varieties of relational database management systems (MySql, PostgreSQL, SQL Server, Oracle, and I'm sure there are more)

**Elastic Load Balancing (ELB)** - main function is to direct and route traffic to your EC2 compute resources (combined with auto scaling). Any traffic going to your website is directed to the ELB and then route appropriately. If one of your servers fails, the ELB will appropriately reroute any traffic (across multiple availability zones as well). There are both external and internal load balancers. An external will be used for routing traffic from the web; internal for traffic only within your AWS VPC.

**Bean Stalk** - takes your uploaded web application code and automatically provisions and deploys the appropriate resources to make the web application operational (EC2, route53, autoscaling, ELB, etc.)


**ECS (EC2 Container Service)** - run Docker enabled applications packaged as containers across a cluster of EC2 services. 

**Batch** - primarily used in specialty cases where a huge amount of compute power across a cluster of compute resources to complete batch processing executing a series of jobs or tasks

**Lightsail** - a virtual private server (VPS) backed by AWS infrastructure. Designing to be simple, easy, and quick to use. Used to host simple websites and blogs usually. 

**Amazon Machine Images (AMI)** - basically an autoconfigured EC2 instance


<hr>

### Storage

**Simple Storage Service (S3)** - organizes content in buckets. You can store video files, backups, mp3s, html, css, js, ANYTHING. The size can range from 0 bytes to 5 TBs. 

**Identity and Access Mgmt (IAM)** - allows you to restrict permissions to specific buckets (list, upload/delete, view permissions)

**RDS** - relational database that offers most standard services (MySQL, PostgreSQL, etc.). It basically takes away the administrative services associated with a database. 
