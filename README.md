# Create infra with CFT and automation to copy file through ansible


1) Create VPC and Subnet
```
aws cloudformation create-stack --stack-name DevOpsDemo-dev-vpc --template-body file://DevOpsDemo-VPC.json --parameters file://DevOpsDemo-VPC-Parameters.json
```
2) Create Public EC2 instance with Jenkins and ansible
```
aws cloudformation create-stack --stack-name DevOpsDemo-dev-PublicInstance --template-body file://Public-Subnet1-EC2-instance-CFT.json --parameters file://Public-Subnet1-EC2-instance-Parameters.json
```
3) Create Private EC2 instance
```
aws cloudformation create-stack --stack-name DevOpsDemo-dev-PrivateInstance --template-body file://Private-Subnet1-EC2-instance-CFT.json --parameters file://Private-Subnet1-EC2-instance-Parameters.json
```
4) setup login details for Jenkins , You can find jenkinURL from output of Publicinstance stack
5) Keep Key of PrivateInstabce to run ssh/ansible playbook in /etc/ansible
6) configure inventroy file on PublicInstance in /etc/ansible ( you can find IP of PrivateInstance from Privateinstance stack)
```
   #cd /etc/ansible
 ```
  A)
  ```
  #cat hosts
        [privateinstance]
        10.10.0.149 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=EC2-test.pem
 ```
 B) Check Private machine reachablity from Publicmachin using ansible
 ```
     #ansible -m ping privateinstance
 ```

7) Now Create Job in Jenkin server to create Dockerfile and keep it in /mnt/artefact
    copy Build steps from file Jenikins-Job-Shell for Execustion-Shell build step
    ```
    #cat jenkins/Jenikins-Job-Shell
    ```
    

8) run ansible-playbook from PublicInstance 
```
   #cd /etc/ansible
   #ansible-playbook PrivateInstance.yaml 
 ```
