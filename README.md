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
- 
- Availability Zone: Choose the same Availability Zone as the EC2 instance you want to attach the volume to.
Volume Type: Select the appropriate volume type based on your performance and cost requirements.
Size: Specify the size of the volume in gigabytes (GB).
