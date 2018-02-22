### Create an elasticache cluster

# (This tutorial was created by following along from Cloud Academy)

<hr>

### Step 1: Create a cache subnet group

An ElastiCache Subnet Group is a collection of subnets that can be assigned to any ElastiCache cluster running in an Amazon Virtual Private Cloud (VPC) environment. 
ElastiCache uses that cache subnet group to select a subnet and IP addresses within that subnet to associate with your cache nodes.

Go to `create subnet group` 

1) Give it a name
2) Give it a description
3) Assign it to a VPC
4) Pick an AZ
5) Assign a subnet ID

ElastiCache enables you to set up, manage, and scale a distributed in-memory cache environment in the cloud. 
It provides a high-performance, resizable, and cost-effective caching solution, while removing the complexity associated with deploying and managing a distributed cache environment. 
You can choose from Memcached or Redis protocol-compliant cache engine software, and let ElastiCache perform software upgrades and patch management for you automatically.

<hr>

### Step2: Create a new Elasticache cluster powered by Memcached

1) Go to the ElastiCache Dashboard and click `get started now`
2) Select `Memcached`
3) Select latest engine version, change node type to `cache.t2.micro` and number of nodes to 2. Everything else can be default
4) In advanced settings, choose the subnet group you created.

**Create** -- it may also ask you about availability zone selection too. Simple fix in the advanced settings.

<hr>

### Step3: Launch an EC2 instance

Go to EC2 and just pick the free tier micro AMI.

Configure the instance details and pick one of the subnets you created. 

Keep everything else the same and create your instance. SSH into that instance using your key.

<hr>

### Step 4: Configure the security group

The rules of a Security Group control the inbound traffic that's allowed to reach the instances that are associated with the security group and the outbound traffic that's allowed to leave them. 
By default, security groups allow all outbound traffic and disallow all inbound one.

1) Go to security groups and click on default.
2) Click on inbound at the bottom and select edit
3) Add a rule with the following:
* Type: Custom TCP Rule
* Protocol: TCP
* Port: 11211
* Source: 172.31.0.0/16
4) Click save

<hr>

### Step 5: Install Elasticache Memcached extension for PHP

AWS Team developed an enhanced version of the Memcached connector adding the auto-discovery feature. 
The AWS Memcached connector is able to automatically identify all of the nodes in a cache cluster, and to initiate and maintain connections to all of these nodes. 
With Auto Discovery, the application does not need to manually connect to individual cache nodes; instead, it connects to a configuration endpoint. 
The configuration endpoint DNS entry contains the CNAME entries for each of the cache node endpoints.

Do the following steps:

1) sudo yum -y update
2) sudo yum install -y gcc make gcc-c++ php php-devel php-pear
3) Now you need to download and install the right version of the Memcached connector. 
Check with `uname -an` and if you see `x86_64` then you know you're on a 64 bit processor. 
4) Check your PHP version: `php -v`. You'll see something like `PHP 5.3.29`
5) You know the PHP version of the AMI (for me at least) is 64bit 5.3.29
6) Go back to the dashboard on AWS and select Elasticache Memcached Cluster **Client**
7) Select your PHP version
8) You now need to upload that client using SCP. This is a tough one so pay attention:
9) Open up another terminal where you are NOT SSH'd into your ec2 instance.
10) I will give the spots where you should type in your own info and then my complete example below. Sorry for the bad layout,
I wanted to make sure you got the spacing correct.

```
scp -i YOUR-KEY.pem AmazonElastiCacheClusterClient-X.Y.Z-PHP53-64bit.tgz(the thing you just downloaded) ec2-user@EC2-Instance-IP:/home/ec2-user/
```

```
scp -i /Users/shannonlucas/Documents/linux/elasticacheKey.pem /Users/shannonlucas/Downloads/AmazonElastiCacheClusterClient-1.0.1-PHP53-64bit.tgz ec2-user@54.213.58.32:/home/ec2-user 
```

11) Install the package: `sudo pecl install /home/ec2-user/AmazonElastiCacheClusterClient-X.Y.Z-PHP53-64bit.tgz` 
12) Run the following command to enable the Elasticache client (in your SSH'd terminal, not the one you SCP'd):

```
sudo /bin/sh -c 'echo "extension=amazon-elasticache-cluster-client.so" >> /etc/php.ini'
```
13) If you want to confirm it appended, feel free to use: `cat /etc/php.ini | grep -n amazon`
14) DONE WITH THIS STEP. Whew.

<hr>

### Step 6

1) Download this demo client script `wget http://bit.ly/1vf3vQx -O elasticache-client.php`
2) Go to your ca-cache cluster and get the endpoint: `ca-cache.nt430g.cfg.usw2.cache.amazonaws.com:11211`
3) Type in: `php elasticache-client.php --endpoint=ca-cache.nt430g.cfg.usw2.cache.amazonaws.com:11211`
4) You'll see some output about connecting to the 2 nodes you created. 
5) You succeeded, now delete the cache by selecting delete in the memcached screen on the elasticache dashboard















