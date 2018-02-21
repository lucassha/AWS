### Creating an RDS 

**Step 1**

Create a subnet. Make sure you select all availability zones, as an RDS needs at least 2, to ensure redundancy

**Step 2**

Next, create an RDS. You can choose between any number of RDBMS(s?). For this, I chose MySQL

Choose dev/test - MySQL for the use case.

For the DB details, you only need to change `DB Instance class` to `db.t2.micro`, which should be at the very top. 

Then choose an identifier, username and password. 

You'll have a few more options to choose from in the next page, but everything can be kept to default. Create your DB instance.

**Step 3**

We need to add an inbound rule to the VPC Security Group created during the RDS instance.

You can get to it by going to the following:

* VPC 
* Security: Security Groups

Once you're there, you should see the RDS that you named. For instance, my Group Name is `rds-launch-wizard`. 

Click on `inbound rules` on the bottom and let's have a look. Type in the following, and you're good to go:

```
**Type**: MYSQL
**Protocol**: TCP
**Port**: 3306
**Source**: 172.31.0.0/16
```

Now, let's launch an EC2 instance. Just choose the basic Linux 64 bit AMI and keep reviewing until you hit `Configure Instance Details`.
There, you want to make sure one of your Subnets is select and that auto-assign Public IP is also enabled. 

Now, keep reviewing until you hit `Configure Security Group`. Add a rule with type `All ICMP - IPv4`. You'll want to select the source to `Anywhere`.
We are doing this just so we can later do a ping test. 

Now configure this instance and get yourself a key, or use one you already have set up. 

Once you're configured, install MySQL with `sudo yum install mysql -y` 

After, let's go back to the RDS instance and find its endpoint link. There's a lot of info there, so `ctrl + f` is your friend. 

Type in your credentials and boom you're connected. You can now make tables in the DB!



