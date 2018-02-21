### How to mount an EBS instance in a Linux EC2 instance

Type in `lsblk` to make sure your EBS volume(s) has been created 


**Give the volume a file extension type of ext4:**

`sudo mkfd -t ext4 /dev/xvdf`

**Create a mounting location for ebs volumes:**

`sudo mkdir /mnt/ebs-store`

**Mount your volume in** `ebs-store`**:**

`sudo mount /dev/xvdf /mnt/ebs-store`

**Check to make sure it's mounted:**

`df -h`

or

`lsblk`
