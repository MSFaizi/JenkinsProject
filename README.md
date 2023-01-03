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

- yum install docker -y
- systemctl enable docker
- systemctl start docker

Step-4: DOCKER-HOST 
- ec2-user
- sudo su
- hostnamectl set-hostname jenkins
- bash
- yum install docker -y
- systemctl enable docker
- systemctl start docker
- systemctl status docker
- vi /etc/ssh/sshd_config \
Note: Vi editor will be open, change below point - 
1. Uncomment 'PermitRootLogin yes'
2. Change PasswordAuthentication no to yes
- press ESC button
- :wq (To save and exit from vi editor)
- systemctl reload sshd
- passwd root
Note: Set password as per your convenience

SSH connection part 

Step-5: JENKINS-SERVER (connection between jenkins server to ansible server)
- ssh-keygen
- ssh-copy-id -i root@[private IP of ANSIBLE-SERVER]
- ssh root@[private IP of ANSIBLE-SERVER]

Step-6: ANSIBLE-SERVER (connection beteen ansible server to docker hub)
- ssh-keygen
- ssh-copy-id -i root@[private IP of DOCKER-HUB]
- ssh root@[private IP of DOCKER-HUB]

Step-7: Go to Jenkins Dashboard -> Manage Jenkins -> Manage Plugins -> Available plugins \
Search ssh, Find Public Over SSH - Install and restart

Step-8: Manage Jenkins -> Configure System -> Scroll down to SSH servers -> Add \
Name - jenkins \
Hostname - private IP of jenkins server \
Username - root \
Click on Advance -  \
Tick on 'Use password authentication, or use a different key' \
Type Password that we had set \
Scroll Down and click on "Test Configuration" \
If password is correct "SUCCESS" message will be displayed  

Click on ADD \
Name - ansible \
Hostname - private IP of ansible server \
Username - root \
Click on Advance -  \
Tick on 'Use password authentication, or use a different key' \
Type Password that we had set \
Scroll Down and click on "Test Configuration" \
If password is correct "SUCCESS" message will be displayed \
Apply & Save
































