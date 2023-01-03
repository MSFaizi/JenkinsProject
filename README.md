# Project Scenario:
![image](https://user-images.githubusercontent.com/102685509/210368764-2a070a92-79ea-4436-87e9-0ee505d5ac44.png)

Pre-requisites:
1. Login into GitHub account
2. Login into Docker Hub account
3. Login into AWS account

Step-1: Create 4 ec2 instances in AWS account as shown in below pic and give same name as it is- 
![image](https://user-images.githubusercontent.com/102685509/210373148-3291e72a-25c9-44f5-880f-15cae0a1bb6b.png)

Take access of all server one by one usig Putty

Step-2: JENKINS-SERVER
- ec2-user
- sudo su
- hostnamectl set-hostname jenkins
- bash
- yum install java* -y
- wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
- rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
- yum install jenkins
- systemctl status jenkins
- systemctl enable jenkins
- systemctl start jenkins
- systemctl status jenkins

