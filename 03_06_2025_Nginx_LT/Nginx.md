# Hands-on EC2-02 : How to Install Nginx Web Server on EC2 Linux 2

Purpose of the this hands-on training is to give the students basic knowledge of how to install Nginx Web Server on Amazon Linux 2 EC2 instance.

## Learning Outcomes

At the end of the this hands-on training, students will be able to;

- demonstrate their knowledge of how to launch AWS EC2 Instance.

- establish a connection with AWS EC2 Instance with SSH.

- install the Nginx Server on Amazon Linux 2 Instance.

- configure the Nginx Server to run simple HTML page.

- write a simple bash script to run the Web Server

- automate the process of installation and configuration of a Web Server using the `user-data` script of EC2 Instance.

## Outline

- Part 1 - Launching an Amazon Linux 2 EC2 instance and Connect with SSH

- Part 2 - Installing and Configuring Nginx Web Server to Run a Simple Web Page

- Part 3 - Automation of Web Server Installation through Bash Script

## Part 1 - Launching an Amazon Linux 2 EC2 instance and Connect with SSH

1.  Launch an Amazon 2 EC2 instance with AMI as `Amazon Linux 2023`, instance type as `t2.micro` and security 
group which allows connections from anywhere for port 22(SSH) and port 80(HTTP).

2. Connect to your instance with SSH.

```
ssh -i [Your Key pair] ec2-user@[Your EC2 IP / DNS name]
```

## Part 2 - Installing and Configuring Nginx Web Server to Run a Simple Web Page

1. Update the installed packages and package cache on your instance.
```
sudo dnf update -y
```
2. Install the Nginx Web Server.
```
sudo dnf install nginx -y
```

3. Start the Nginx Web Server.
```
sudo systemctl start nginx
```
4. Check from browser with public IP/DNS


5. Go to /usr/share/nginx/html folder.
```
cd /usr/share/nginx/html
```
6. Show content of folder and change the permissions of /usr/share/nginx/html
```
ls
sudo chmod -R 777 /usr/share/nginx/html
```
7. Remove existing `index.html`.
```
sudo rm index.html
```
8. Upload new `index.html` and `ken.jpg` files with `wget` command. Show the github and explain the RAW .

```
Github Repo: " https://github.com/awsdevopsteam/route-53 "
wget https://raw.githubusercontent.com/awsdevopsteam/route-53/master/index.html
wget https://raw.githubusercontent.com/awsdevopsteam/route-53/master/ken.jpg
```
9. restart the Nginx Web Server.
```
sudo systemctl restart nginx
```
10. configure to start while launching
```
sudo systemctl enable nginx
```
11. Check if the Web Server is working properly from the browser.

12. to add another content change the permissions of folder /usr/share/nginx/html.(If you haven't before)
```
sudo chmod -R 777 /usr/share/nginx/html
```
# The command chmod -R 777 / makes every single file on the system under / (root) have rwxrwxrwx permissions. This is equivalent to allowing ALL users read/write/execute permissions.
13. Add another index.html file 
```
echo "Second Page" > /usr/share/nginx/html/index_2.html
```
14. add "/index_2.html" at the end of the the public DNS 
For Example: http://ec2-54-144-132-10.compute-1.amazonaws.com/index_2.html
ls
## Part 3 - Automation of Web Server Installation through Bash Script (User data)
15. Launch an Amazon 2 EC2 instance with AMI as `Amazon Linux 2023`, instance type as `t2.micro` and security group which allows connections from anywhere for port 22(SSH) and port 80(HTTP).
Your instance is launched with an Amazon Linux 2 AMI. These instructions are intended for use with Amazon Linux 2, and the commands and directives may not work for other Linux distributions.
16. Configure instance to automate web server installation with `user data` script.
```
#! /bin/bash
dnf update -y
dnf install nginx -y
systemctl start nginx
cd /usr/share/nginx/html
chmod -R 777 /usr/share/nginx/html
rm index.html
wget https://raw.githubusercontent.com/awsdevopsteam/route-53/master/index.html
wget https://raw.githubusercontent.com/awsdevopsteam/route-53/master/ken.jpg
systemctl restart nginx
systemctl enable nginx
```

17. Review and launch the EC2 Instance
18. Once Instance is on, check if the Nginx Web Server is working from the web browser.
19. Connect the Nginx Web Server from the terminal with `curl` command.
```
curl http://ec2-3-15-183-78.us-east-2.compute.amazonaws.com
```
