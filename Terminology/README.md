### Basic Terminology

**Elastic Book Store (EBS)** - provides persistent block level storage volumes for use with EC2 instances in the AWS Cloud. Each EBS volume is automatically replicated within its Availability Zone to protect you from component failure

**Relational Database Service (RDS)** - web service that makes it easy to set up, operate, and scale a relational database in the cloud. Offers access to many varieties of relational database management systems (MySql, PostgreSQL, SQL Server, Oracle, and I'm sure there are more)

**Elastic Load Balancing (ELB)** - main function is to direct and route traffic to your EC2 compute resources (combined with auto scaling). Any traffic going to your website is directed to the ELB and then route appropriately. If one of your servers fails, the ELB will appropriately reroute any traffic (across multiple availability zones as well). There are both external and internal load balancers. An external will be used for routing traffic from the web; internal for traffic only within your AWS VPC.
