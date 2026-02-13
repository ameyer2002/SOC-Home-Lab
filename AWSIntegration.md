# Connecting CloudTrail, S3, an EC2 Instance, and a VPC

Because I want this SOC to be hybrid, I will be connecting AWS to it, specifically using CloudTrail, S3, an EC2 Instance, and a VPC. Down the line, I will likely setup more services to understand how they work in conjuction with a SOC.

The first thing I am going to setup is a VPC with 1 availability zone and 1 public subnet. I am going to put my EC2 instance in this subnet but secure it via security groups.
The first thing I am going to do is create a trail in CloudTrail. CLoudTrail is an AWS service that 

<img width="1920" height="903" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/600935ef-d44e-42c8-97a2-27759b24f188" />

Immediately following the creation of the trail, a S3 bucket is created to store those logs being ingested CloudTrail.

<img width="1920" height="877" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/0f4f62de-cf3e-4323-b5a0-0f29f3a7b1bc" />
