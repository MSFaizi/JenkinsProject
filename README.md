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
- systemctl status jenkins \
Note: Copy public IP of JENKINS-SERVER and paste in browser with port 8080. Further it will ask for Administration password- Copy path given above and use below command
- cat [paste copied path] \
Note: After using above command, password will be displayed copy that and paste in Administration Pasword field and choose Continue & Install suggested plugins
- passwd root \
Note: Set password as per your convenience
- vi /etc/ssh/sshd_config 

Note: Vi editor will be open, change below point - 
1. Uncomment 'PermitRootLogin yes'
2. Change PasswordAuthentication no to yes
- press ESC button
- :wq (To save and exit from vi editor)
- systemctl reload sshd

Step-3: ANSIBLE-SERVER
- ec2-user
- sudo su
- hostnamectl set-hostname ansible
- bash
- sudo amazon-linux-extras install ansible2
- passwd root \
Note: Set password as per your convenience
- vi /etc/ssh/sshd_config 

Note: Vi editor will be open, change below point - 
1. Uncomment 'PermitRootLogin yes'
2. Change PasswordAuthentication no to yes
- press ESC button
- :wq (To save and exit from vi editor)
- systemctl reload sshd
- vi /etc/ansible/hosts \
Note: vi edior will be open, mention below line \
[DOCKER-HOST] \
172.31.86.212 (private Ip of docker host)

![image](https://user-images.githubusercontent.com/102685509/210386810-1c4c392c-39ef-437b-ae73-99f66f34886d.png)


