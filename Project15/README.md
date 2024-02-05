# AWS Networking Implementation (VPC, SUbnets, IG, NAT, Routing)
In this project, we will master the art of AWS networking implementation, including VPC, subnets, internet gateways, NAT, and routing which enables us to design and deploy scalable and secure cloud architectures. 

## VPC Creation and Subnet configuration

In this field, we will use Virtual Private Clouds (VPC) and subnets to create the backbone of our cloud-based projects. In this article, we will simplify the complex aspects of AWS networking, highlighting the useful and adaptable nature of VPC and subnets. 

**What is an Amazon VPC?**

An Amazon Virtual Private Cloud (VPC) is like your own private section of the Amazon cloud, where you can place and manage your resources (like servers or databases). you control who and what can go in and out, just like a gated community.

*The essential steps to creating a VPC and configuring core network services are covered as follows;*

- The default VPC

- Creating a new VPC

- Creating and configuring subnets

**The Default VPC:** This is like a starter pack provided by Amazon for your cloud resources. It's a pre-configured space in the Amazon cloud where you can immediately start deploying your applications or services. It has built-in security and network settings to help you up and running quickly, but you can adjust these as you see fit. 

![default-vpc](images/Def-vpc.png)

A Defaultl VPC, which Amazon provides for you in each region (think of a region as a separate city), is like a pre-built house in that city. This house comes with some default settings to help you move in and start living (or start deploying your applications) immediately. But just like a real house, you can change these settings according to your needs. 

**Creating a new VPC:** As we want to learn step by step and observe the components, choose the "VPC only" option, we'll use the "VPC and more" option later. Enter "first-vpc" as the name tag and "10.0.0.0/16" as the IPV4 CIDR. The "10.0.0.0/16" will be the primary IPV4 block and you can add a secondary IPV4 block e.g., 100.64.0.0/16. The use case of a secondary CIDR block could be because you're running out of IPs and need to add an additional block, or there's a VPC with overlapping CIDR that you need to peer or connect. We can look further to see how a secondary CIDR block is being used in an overlapping IP scenario: [https://aws.amazon.com/blogs/networking-and-content-delivery/how-to-solve-private-ip-exhaustion-with-private-nat-solution/](https://aws.amazon.com/blogs/networking-and-content-delivery/how-to-solve-private-ip-exhaustion-with-private-nat-solution/)

![create-vpc](images/createvpc.png)+

Leave the tags as defaults, we can add more tags if we want and click `CREATE VPC`

![crt-vpc](images/createvpc1.png)

As soon as the VPC is created, it's assigned with a vpc-id and there's a route table created that serves as the main route table - `rtb----` as shown below. 

![crt-vpc](images/createvpc2.png)

Now we have a VPC and a route table, but we won't be able to put anything inside. For example, we can't create an EC2 instance as it requires subnets.

**Creating and configuring subnets:**

*What are subnets?*

Subnets are like smaller segments within a VPC that help you organize and manage your resources. Subnets are like dividing an office building into smaller sections, where each selection represents a department. In this analogy, subnets are created to organize and manage the network effectively. 

![subnets](images/subnet-d.png)

**Subnet name**    | **AZ**   |   **CIDR block**

subnet-public1a   |  eu-north-1a  |   10.0.11.0/24

subnet-public2b  |   eu-north-1b |    10.0.12.0/24

subnet-private1a   | eu-north-1a  |   10.0.1.0/24

subnet-private2b  |  eu-north-1b   |  10.0.2.0/24

Go to VPC > Subnets > Create Subnets and select the VPC that you've created previously the "first-vpc"

![subnets](images/subnets.png)

click on `CREATE SUBNET`

![subnets1](images/subnets1.png)

Enter the subnet settings details. we do not click the "Create subnet" button just yet, click the Add new subnet button to add the remaining subnets then after completing all the required subnets, click **"Create subnet"** Note: if you don't choose a zone, it will be randomly picked by AWS.

![subnets2](images/subnet2.png)

![subnets3](images/subnets3.png)

![subnets4](images/subnets4.png)

Once done, we should see all the subnets just created on the console. As of now, we can deploy EC2 instances into the VPC by selecting one of the subnets, but the public subnet doesn't have any internet access at this stage. When selecting a public subnet, we see it uses the main route table and only has the local route, no default route for internet access. 

![subnets5](images/subnets5.png)

**Understanding Public and Private Subnets in AWS VPC**

In the world of AWS VPC, think of subnets as individual plots in your land (VPC). Some of these plots(subnets) have direct road access (internet access) - these are public subnets. Others are more private, tucked away without direct road access - these are private subnets. 

**Creating a Public Subnet**

Creating a Public Subnet is like creating a plot of land with direct road (internet) access. Here's how you do it:

- Go to the AWS VPC page.

- Find 'Subnets', click on it, then click 'Create Subnet.'

- Give this new plot a name, select the big plot (VPC) you want to divide and leave the IP settings as they are.

- Attach an Internet Gateway to this subnet to provide the road (internet) access. 

- Update the route table associated with this subnet to allow traffic to flow to and from the internet.

**Creating a Private Subnet**

Creating a private subnet is like creating a secluded plot without direct road (internet) access. Here's how you do it;

- Go to the AWS VPC page.

- Find Subnets, click on it, then click 'Create subnet'. give it a name, select the big plot(VPC) you want to divide and leave the IP settings as they are. 

- Don't attach an internet Gateway to this subnet, keeping it secluded.

- The route table for this subnet doesn't allow traffic to and from the internet. 

**Working with Public and Private SUbnets**

Public subnets are great for resources that need to connect to the internet, like web servers. Private subnets are great for resources that you don't want to expose to the internet, like databases. 

Understanding public and private subnets helps you to organize and protect your AWS resources better. We should always remember to use public subnets for resources that need internet access and private subnets for resources that we want to keep private. 

## Internet Gateway and Routing Table

Technically, the subnets are still private. So we need these to make it work as public subnets;

- An Internet Gateway(IGW) attached to the VPC

- Route table with a default route towards the IGW

- Public IP assigned to the AWS resources (e.g. EC" instances)

Now we navigate to VPC > **Internet gateways** and click **"Create internet gateway"**

![igw](images/IGW.png)

Put a tag name and click Create Internet Gateway

![igw1](images/IGW1.png)

Then we attach the IGW to the VPC

![igw2](images/IGW2.png)

Select the VPC

![igw3](images/IGW3.png)

We want the private subnets to be private, we don't want the private subnets to have a default route to the Internet. For that, we'll need to create a separate route table for the public subnets.

**What is a Routing Table**

A Routing Table is like a map or GPS. It tells the people (data) in your city (VPC) which way to go to reach their destination. For example, if the data has to travel to the Internet, the routing table will tell it to take the road (Internet Gateway) that we built.

**Creating and Configuring Routing Tables**

Now that we have our entrance and exit (Internet Gateway), we need to give direction to our resources. This is done through the Routing Table. It's like a map, guiding your resources on how to get in and out of your VPC.

Let's navigate to the route table menu and create a route table for the public subnets. 

![RT](images/RT.png)

Put a name for the routeing table e.g test-vpc-public-rtb and select the desired vpc - "test-vpc"

![RT1](images/RT1.png)

Once created, edit the route table, add a default route table to the internet gateway(IGW)

![RT2](images/RT2.png)

After that, we select the Internet Gateway

![RT3](images/RT3.png)

Next, go to the **"Subnet associations"** tab and click **"Edit subnet associations"**

![subnet-ass](images/Subnet-ass.png)

Select the public subnets and click **"Save associations"**

![subnet-ass1](images/subnet-ass1.png)

Thats it! Now that the VPC is ready, we can run an EC2 instance in the public subnets if they need internet access or in private subnets if they don't. 

NOTE:

**test-vpc-public-rtb:** A route table with a target to the internet gateway is a public route table.

**test-vpc-private-rtb:** A route table with a target to NAT gateway is a private route table. 

- Now we will also create the route table for private but subnets and routes are not yet attached to it, just only created. 

![RT](images/RT.png)

## NAT Gateway and Private SUbnets

**Introduction to Private Subnets and NAT Gateway**

In your AWS Virtual Private Cloud(VPC), private subnets are secluded areas where you can place resources that should not be directly exposed to the internet. But what if these resources need to access the internet for updates or downloads?
This is where the NAT Gateway comes in. 

A private subnet in AWS is like a secure room inside your house (VPC) with no windows or doors to the street (Internet). Anything you place in this room (like a database) is not directly accessible from the outside world. 

**Understanding NAT Gateway**

A Network Address Translation(NAT) Gateway acts like a secure door that only opens one way. It allows your resources inside the private subnet to access the internet for things like updates and downloads, but it doesn't allow anything from the internet to enter your private subnet.

A Network Address Translation(NAT) allows instances in your private subnet to connect to outside services like Databases but restricts external services from connecting to these instances. 

**Creating a NAT Gateway and Linking it to a Private SUbnet**

We will cover step-by-step guild on how to create a NAT Gateway and how to link it to our private subnet. We'll also cover how to configure a route table to direct outbound internet traffic from our subnet to the NAT Gateway. 

First go to VPC > **NAT Gateways** and click **Create NAT Gateway**

![NAT](images/NAT.png)

Create the NAT Gateway named **test-nat**, under one of the private subnets that was previously created, we choose the **subnet-private1a** as the subnet. Then we need to allocate ELastic IP because it is required for the creation of NAT Gateway

![NAT1](images/NAT1.png)

Now let's go to the route table menu and create a route table for the private subnets. Then we edit the route table and add a default route to the Network Address Translation(NAT) Gateway.

![RT4](images/RT4.png)

Choose route table **RTB-Private**, select Route tab, and select **Add Route**. Under the Target, select the NAT Gateway named **test-nat.**

![RT5](images/RT5.png)

![RT6](images/RT6.png)

![RT7](images/RT7.png)

Next, go to the **Subnet associations** tab and click **Edit subnet associations**

![RT8](images/RT8.png)

![RT9](images/RT9.png)

#### Summary and Best Practices

To conclude, we'll revisit the importance of NAT Gateways in the context of private subnets and summarize the key points of the course. We'll also share some best practices when working with private subnets and NAT Gateways in AWS.

By the end of this course, we should have a clear understanding of how private subnets and NAT Gateways work in AWS and how we can use them to maintain security while allowing necessary internet access for our resources. 

## Security Group and Network ACLs

**Understanding the Difference between Security Groups and Network Access Control List**

Security groups and network access control lists (ACLs) are both important tools for securing your network on the AWS cloud, but they serve different purposes and have different use cases. 

**Security Groups**

![SG](images/SC.png)

Security groups can be compared to a bouncer at a club who controls the flow of traffic to and from your resources in a cloud computing environment. Imagine you have a club, and you want to ensure that only authorized individuals can enter and exit. In this analogy, the club represents your cloud resources (such as virtual machines or instances), and the bouncer represents the security group. 

Just like a bouncer checks the IDs and credentials of people at the club's entrance, a security group examines the IP addresses and ports of incoming and outgoing network traffic. It acts as a virtual firewall that filters traffic based on predefined rules. These rules specify which types of traffic are allowed or denied. 

For example, a security group can be configured to allow incoming HTTP traffic on port 80 to a web server, but block all other types of incoming traffic. Similarly, it can permit outgoing traffic from the webserver to external databases on a specific port, while restricting all other outbound connections. 

By enforcing these rules, security groups act as a line of defence, helping to protect your resources from unauthorized access and malicious attacks. They ensure that only the traffic that meets the defined criteria is allowed to reach your resources while blocking or rejecting any unauthorized or potentially harmful traffic. 

It's important to note that security groups operate at the instance level, meaning they are associated with specific instances and can control traffic at a granular level. They can be customized and updated as needed to adapt to changing security requirements. 

Overall, security groups provide an essential layer of security for your cloud resources by allowing you to define and manage access control policies, much like a bouncer regulates who can enter and exit a club. 

**Network Access Control List (NACLs)**

![NACLs](images/NACLS.png)

Network ACLs (Access Control Lists) can be likened to a security guard for a building, responsible for controlling inbound and outbound traffic at the subnet level in a cloud computing environment. Imagine you have a building with multiple rooms and entry points, and you want to ensure that only authorized individuals can enter and exit. In this analogy, the building represents your subnet, and the security guard represents the network ACL. 

Similar to a security guard who verifies IDs and credentials before allowing entry into the building, a network ACL examines the IP addresses and ports of incoming and outgoing network traffic. It serves as a virtual barrier or perimeter security, defining rules that dictate which types of traffic are permitted or denied. 

For instance, a network ACL can be configured to allow incoming SSH(Secure Shell) traffic (on port 22) to a specific subnet, while blocking all other types of incoming traffic. It can also permit outgoing traffic from the subnet to a specific range of IP addresses on a certain port while disallowing any other outbound connections.

By implementing these rules, network ACLs act as a crucial line of defence, safeguarding your entire subnet from unauthorized access and malicious attacks. They ensure that only traffic meeting the specific criteria is allowed to enter or exit the subnet while blocking any unauthorized or potentially harmful traffic. 

It's important to note that network ACLs operate at the subnet level, meaning they control traffic for all instances within a subnet. They provide a broader scope of security compared to security groups, which operate at the instance level. Network ACLs are typically stateless, meaning that inbound and outbound traffic is evaluated separately, and specific rules must be defined for both directions. 

In summary, network ACLs function as a virtual security guard for your subnet, regarding inbound and outbound traffic at a broader level. They operate similarly to a security guard who controls access to a building by examining IDs, ensuring that only traffic meeting the defined rules is allowed to pass, and thereby providing protection against unauthorized access and malicious activities for your entire subnet. 

**In conclusion**

![vpg1](images/vpg1.png)
![vpg2](images/vpg2.png)

In short, security groups and network ACLs are both important tools for securing your network on the AWS cloud, but they serve different purposes and have different use cases. Security groups are like bouncer at a club, controlling inbound and outbound traffic to and from your resources at the individual resources level. Network ACLs, on the other hand, are like security guards for a building, controlling inbound and outbound traffic at the subnet level.

**VPC Peering and VPN Connection**

**Introduction to VPC Peering**

![vpc-peer](images/vpc-peer.png)

VPC Peering is a networking feature that allows you to connect two Virtual Private Clouds(VPCs) within the same cloud provider's network or across different regions. VPC Peering enables direct communication between VPCs, allowing resources in each VPC to interact with each other as if they were on the same network. It provides a secure and private connection without the need for internet access. VPC Peering is commonly used to establish connectivity between VPCs in scenarios such as multi-tier applications, resource sharing, or data replication. 

**Benefits of VPC Peering**

- Simplified Network Architecture: VPC Peering simplifies network design by enabling direct communication between VPCs, eliminating the need for complex networking configurations. 

- Enhanced Resource Sharing: With VPC Peering, resources in different VPCs can communicate seamlessly, allowing for efficient sharing of data, services, and applications. 

- Increased Security: Communication between peered VPC remains within the cloud provider's network, ensuring a secure and private connection. 

** Low Latency and High Bandwidth: ** VPC Peering enables high-performance networking with low latency and high bandwidth, improving application performance. 

**- Cost Efficiency:** Utilizing VPC, Peering eliminates the need for additional networking components, reducing costs associated with data transfer and network infrastructure. 

**Introduction to VPN Connections**

VPN (Virtual Private Network) connections establish a secure and encrypted communication channel between your on-premises network and a cloud provider's network, such as a VPC. VPN connections enable secure access to resources in the cloud from remote locations or connect on-premises networks with cloud resources.

*There are two primary types of VPN connections:*

**1. Site-to-Site VPN:** Site-to-site VPN establishes a secure connection between your on-premises network and the cloud provider's network. It allows communication between on-premises resources and resources in the VPC securely and privately. This type of VPN connection is commonly used in hybrid cloud architectures.

![vpn1](images/vpn1.png)

**2. AWS Client VPN:** AWS Client VPN provides secure remote access to the cloud network for individual users or devices. It enables secure connectivity for remote employees, partners, or contractors to access resources in VPC securely. 

![vpn2](images/vpn2.png)

**Benefits of VPN Connections**

- **Secure Remote Access:** VPN connections enable access to resources in the cloud network for remote users or devices, ensuring data privacy and protection.

- **Data Encryption:** VPN connection encrypts the data transmitted between the on-premises network and the cloud network, providing a secure channel for data transfer. 

- **Flexibility and Mobility:** VPN connections allow authorized users to securely access cloud resources from any location, promoting flexibility and mobility in accessing critical applications and data.

- **Hybrid Cloud Connectivity:** VPN connection plays a vital role in establishing secure and reliable connectivity between the on-premises network and cloud resources, facilitating hybrid cloud architectures and seamless integration.

**Summary**

In summary, VPC Peering enables direct communication between VPCs, simplifying network architecture and enhancing resource sharing within the cloud network. VPN connection establishes secure tunnels between on-premises network and the cloud, enabling secure remote access and facilitating hybrid cloud connectivity. Both VPC Peering and VPN connections contribute to building secure, scalable, and efficient network infrastructures in cloud environments. 

