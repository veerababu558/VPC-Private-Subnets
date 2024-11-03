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
- In the AWS Management Console, navigate to VPC.
- Click on Create VPC.
- Under Resource to create, select VPC and more.
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
    Image 9
* Select the "ubuntu" OS type AMI
    Image 10
* Select the "vpc-key-pair-001", the custom VPC that was created and the public subnet.
    Image 11
* Create a security group with port number 22 opened.
    Image 12
* Click on the "Launch instance",The Bastion host is created successfully.
    Image 13
* Log in to the Bastion Host using the SSH command.
     ssh -i <key pair name> ubuntu@<IP address>
    Image 14
* Successfully log in to the Bastion host launched in the public subnet.
    Image 15
* Copy the key pair file to the Bastion host, as we need to connect to the EC2 instances created in the private subnet ,create HTML file, and run the Python Server.
    scp -i<key pair name>  <key pair name> ubuntu@<IP address>:/home/ubuntu
    key pair file is copied successfully.
    Image 16
*  Logging into the first private instance using the SSH command.
    Image 17
* Create a sample .HTML file using vi editor.
    Image 18
*  Run the Python server using the following command.
       python3 -m http.server 8000
    Image 19
## 4. Creation of Load Balancer:  
* In the AWS Management Console, navigate to EC2.
* Click on "Load Balancer" in the left pane and select "Create" to choose "Application Load Balancer"
    Image 20
* Provide the load balancer name as “project-lb-001,” select the custom VPC created, and choose the public subnets.
  Image 21
* Choose a target type as "Instances"
  Image 22
* Provide the target group name as "project-tg-001" and enter the port number as 8000, as our application runs on this port.
  Image 23
* Enter the port number as 8000, click on "Include as pending below" and then click on the "Create target group".
  Image 24
* Target group is created successfully.
  Image 25
* Navigate back to the Load Balancer page, click on refresh, select the newly created target group from the dropdown, and click on 'Create Load Balancer.'
  Image 26
* The Load Balancer is created successfully,however,it is unable to reach the instances because port 80 is not open in the previosuly selected security group.Below is the screenshot.
  Image 27
* Add port 80 to the security group rule, allowing the load balancer to reach the instances now.
  Image 28
## 5. Testing
* Open a web browser, enter the Load balancer endpoint, and press the Enter. Response comes from instance 1.
  Image 29
* Open another web browser window, enter the ELB endpoint, and press Enter. The ELB tries to forward the traffic to the second instance; however, it is unable to reach it because the application server is not running yet
     
     
     


         
        
