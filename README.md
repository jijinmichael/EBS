## EBS
EBS stands for Amazon Elastic Block Store. It is a block-level storage service offered by Amazon Web Services (AWS). EBS provides persistent and highly available block storage volumes that can be attached to Amazon EC2 instances.

EBS is a fundamental component of the AWS infrastructure and is widely used for various purposes, such as hosting databases, storing application data, and supporting other storage-intensive workloads in the cloud.

Let's see some key characteristics and features of EBS:
- **Block-Level Storage:** EBS offers block storage, which means it provides raw storage volumes that function similarly to physical hard drives or SSDs. These volumes can be formatted with a file system and used as persistent storage for EC2 instances.
- **Persistence and Durability:** EBS volumes are designed for durability and data persistence. They provide long-term storage for your data even if the associated EC2 instance is stopped or terminated.
- **Elasticity and Scalability:** With EBS, you can easily scale the size of your storage volumes as your needs change. You can increase or decrease the volume size without impacting the running EC2 instances.
- **Availability and Redundancy:** EBS volumes are replicated within an Availability Zone (AZ) to provide high availability and protection against hardware failures. You can also enable multi-AZ replication to replicate volumes across multiple AZs for further resilience.

## Creating a Volume and attaching to an Instance.

To create an EBS volume and attach it to an EC2 instance, you can follow these steps:

- Open the AWS Management Console and navigate to the EC2 service.
- Click on "Volumes" in the left-hand menu under "Elastic Block Store."
- Click on the "Create Volume" button.
- In the "Create Volume" dialog, specify the desired settings for the volume:
  - **Availability Zone:** Choose the same Availability Zone as the EC2 instance you want to attach the volume to.
  - **Volume Type:** Select the appropriate volume type based on your performance and cost requirements.
  - **Size:** Specify the size of the volume in gigabytes (GB).

In this case my Ec2 Instance is created on ap-south-1b. So I'm creating the additional volume on the same region. Please see below.

![image](https://github.com/jijinmichael/EBS/assets/134680540/fe234cd3-d666-4baa-a018-e235e0a7495e)

For better understanding I have given the name tag as add-vol for the new volume.

Now let us see how to attach this volume to an Instance which we already have.

- Once the volume is created, go back to the "Volumes" page and select the newly created volume.
- Click on the "Actions" dropdown menu and choose "Attach Volume."
- In the "Attach Volume" dialog, select the EC2 instance you want to attach the volume to from the "Instance" dropdown menu.
- Click on the "Attach" button to attach the volume to the instance.

![image](https://github.com/jijinmichael/EBS/assets/134680540/6eb0c729-c176-457d-9957-09bff7452eaf)

Once attached, the volume will appear as a new block device on the EC2 instance.

To check this Log in to the EC2 instance, and use commands like lsblk.
```
[ec2-user@ip-172-31-7-15 ~]$ lsblk 
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0   8G  0 disk 
├─xvda1   202:1    0   8G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part 
xvdf      202:80   0   1G  0 disk 
```
In the above snippet you can see an additional disk named xvdf with 1G. Now we need to format and mount the additional volume.

Here I'm showing a scenario that a client want an additional volume and mount his/her web doc root /var/www/html to the additional volume.

<p align="center">
  <img src="https://github.com/jijinmichael/EBS/assets/134680540/f390a02d-ea48-492c-a9cc-7aa4febbd41c"></p>
  
Partition the attached disk and make the file system to ext4.

```
sudo fdisk /dev/xvdf

Welcome to fdisk (util-linux 2.37.4).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xb4fc930c.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): 

Using default response p.
Partition number (1-4, default 1): 
First sector (2048-2097151, default 2048): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-2097151, default 2097151): 

Created a new partition 1 of type 'Linux' and of size 1023 MiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
[ec2-user@ip-172-31-7-15 ~]$ sudo mkfs -t ext4 /dev/xvdf1
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 261888 4k blocks and 65536 inodes
Filesystem UUID: 5b3099c9-63b0-43c2-a747-ffc1c423e9cd
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```




