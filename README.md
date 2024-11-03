# VPC-Private-Subnets

# VPC with Servers in private subnets

### Project Overview:
This project demonstrates the deployment of applications within private subnets on AWS, configuring auto-scaling to handle varying workloads, and setting up an Elastic Load Balancer (ELB) to distribute incoming traffic across healthy instances. This setup enhances security by restricting direct internet access to the instances, and the load balancer manages traffic distribution across healthy instances to ensure high availability and fault tolerance.

### Prerequisites:
  AWS account
  
### AWS Services:
* Virtual Private Cloud(VPC)
* Auto Scaling Group(ASG)
* Bastion Host(EC2)
* Elastic Load Balancer(ELB)
* Elastic Compute Cloud(EC2)

### Project Architecture:
   Image1
   
## Steps
## 1. Creation of AWS Virtual Private Cloud(VPC):
     *In the AWS Management Console, navigate to VPC.
     * Click on Create VPC.
     * Under Resource to create, select VPC and more.
     Image 2
     * Leave all other options at their default and click on "Create VPC".
     Image 3
     * The VPC is created successfully with 2 public and 2 private subnets across 2 availability zones.
     Image 4
     
## 2. Creation of Auto Scaling Group:
     * In the AWS Management Console, navigate to EC2.
     * Click on "Auto Scaling" in the left pane
     Image 5
     * Provide the Auto Scaling group name as "project-asg-a-001" and click on "Create a launch template."
     Image 6
     * Provide the launch template name and select the Ubuntu instance type, then select the “vpc-key-pair-001.”
     * Select the custom VPC that was created and the security group with ports opened for 22 and 8000 (the application is running on port 8000).
     * Click on the “Create launch template.” The launch template is created successfully.
     * Navigate to the Auto Scaling group page, refresh “Launch templates,” and select the newly created launch template, custom VPC, and private subnets. Set the          desired capacity to 2, the minimum capacity to 2, and the maximum capacity to 2.
     Image 7
     * Click on the "Create Auto Scaling group."
     * The Auto Scaling is created successfully.
     Image 8
  ## 3. Creation of Bastion Host:
     * In the AWS Management Console, navigate to EC2.
     * Click on the "Launch instance" button.
     * Provide the instance name as "project-bastion-host-001."
     
     
     


         
        
