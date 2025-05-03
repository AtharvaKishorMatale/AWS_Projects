# 🧱 VPC 3-Tier Architecture Setup - Step-by-Step
- This setup is done on AWS to host applications securely and efficiently by separating the system into three parts: Web, App, and Database.

# 1. Create a VPC (Virtual Private Cloud)
- What it does:
- It creates your own isolated network inside AWS to launch resources (like servers) securely.
- ![Screenshot 2025-05-01 164118](https://github.com/user-attachments/assets/6ab94d0d-7f43-4b29-85df-00e36d3e0f6b)

# 2. Create Subnets
- Public Subnet: Used for internet-facing components (like web servers).
- Private Subnet: Used for backend components (like app servers and database).
- What it does:
- Subnets divide the VPC into smaller sections. Public ones can talk to the internet, private ones can’t unless you give them special access.
 ![Screenshot 2025-05-01 171255](https://github.com/user-attachments/assets/bebc34d9-d052-4c9d-a4ae-b492737c2acf)


# 3. Create an Internet Gateway
- What it does:
- Allows resources in the public subnet (like web servers) to connect to the internet.
![Screenshot 2025-05-01 170837](https://github.com/user-attachments/assets/ac150258-1c9c-40a6-8688-1fa983b804b0)

# 4. Attach Internet Gateway to VPC
- What it does:
- Connects your VPC to the internet through the gateway so traffic can flow in and out.
![Screenshot 2025-05-03 142516](https://github.com/user-attachments/assets/0907744d-965f-4506-8768-139e3533ad9c)

# 5. Create a Route Table for the Public Subnet
- What it does:
- This table tells the public subnet how to reach the internet using the Internet Gateway.
![Screenshot 2025-05-01 171255](https://github.com/user-attachments/assets/3f77ab12-9542-48a4-bd79-5fca531a9c5c)

# 6. Associate the Public Subnet with the Route Table
- What it does:
- Makes sure the public subnet actually uses the route to reach the internet.
![Screenshot 2025-05-01 171215](https://github.com/user-attachments/assets/34233231-8112-488b-aa6c-ec454632de24)

# Web Server Setup
- Steps:
- Launch EC2 in public subnet with auto-assign public IP.
- Create security group allowing:
- SSH (22), HTTP (80), HTTPS (443).
- Install Apache (or Nginx):
- sudo yum update -y
- sudo yum install httpd -y
- sudo systemctl start httpd
- Access site using public IP in browser.
 ![Screenshot 2025-05-01 171845](https://github.com/user-attachments/assets/f5bbc86d-d6e4-4978-be1e-e26237c14076)

# 9. Create a NAT Gateway in Public Subnet
- What it does:
- Lets the private subnet connect to the internet for updates/downloads but blocks external traffic from directly accessing it.
 ![Screenshot 2025-05-01 173303](https://github.com/user-attachments/assets/9a705992-e70a-4be0-9940-ea5fe6781a5f)

# 10. Update Route Table for Private Subnet
- What it does:
- Routes traffic from private subnet to the internet using the NAT Gateway instead of the Internet Gateway.
![Screenshot 2025-05-01 173939](https://github.com/user-attachments/assets/87cd19a0-81d3-41a5-9103-6eda550a3ca8)

# Appserver setup
# Steps
- Launch EC2 in private subnet, no public IP.
- Create security group to allow:
- SSH only from Web Server.
- SSH into it via Web Server (jump host).

# db-server setup
# 13. Launch RDS (Database) in Another Private Subnet
- What it does:
- Creates a managed database that’s secure and only accessible from the app server.
![Screenshot 2025-05-01 172258](https://github.com/user-attachments/assets/58682d2f-ed1b-44e9-a6d3-0d5168ff22a8)

# 14. Create Security Group for Database
- What it does:
- Ensures only the app server can connect to the database (e.g., allow traffic on port 3306 for MySQL).
![Screenshot 2025-05-01 173046](https://github.com/user-attachments/assets/d9643cc4-cef9-49df-9fd4-96b9b04fb2e4)

# 15. Test Connectivity Between Tiers
- What it does:
Checks that:

- Web server can be accessed from the internet. ![Screenshot 2025-05-01 191952](https://github.com/user-attachments/assets/fe815ccb-e263-4eb6-b105-1c218275aac0)
- Web server can talk to app server.            ![Screenshot 2025-05-01 231559](https://github.com/user-attachments/assets/6c033f2b-e0bb-40ef-81f8-7ec63403f1b7)
- App server can talk to database.              ![Screenshot 2025-05-01 231625](https://github.com/user-attachments/assets/ce54781c-0035-4a95-b653-1d5179ae5007)
