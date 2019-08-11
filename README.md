# Ansible Playbook to Create EC2 Instance

 Automation time So Every want to saving  time and we will use ansible for automation to create instances in AWS Cloud Service.
 This is the simplest way of creating AWS instance using Ansible automation tool.

### Create a EC2 Instance first by AWS Console

We need to create a Ec2 instance with in the aws platform.

### Install Same Packages in Ansible Machine :-
- Ansible
- Python
- Pip

```bash
sudo amazon-linux-extras install ansible2
or
yum install ansible
yum install python-pip

```

### 3. Create a IAM Role to Ansible EC2 Instance and Add :-

You can create the Ec2-instance in the AWS with the policy AmazonEC2FullAccess.

### Attach Role to Ansible EC2 Instance :-
 You can attach the create Role to ec2-instance from Action->instance settings->Attach/replace IAM role.
###  Create a Ansible file for Creating EC2 Instance 

   You can create a .yml file to create the aws instance.
   
   ```python
   
   ---
 - name: 'creating aws instance by ansible code'
   hosts: localhost 
   connection: local
   gather_facts: false
   vars:

     region: us-east-1
     instance_type: t2.micro
     ami: ami-0b898040803850657
     key_name: ansible1
   tasks:

     - name: 'creating ec2-instance'
       ec2:
          key_name: "{{key_name}}"
          instance_type: "{{ instance_type}}"
          image: "{{ ami }}"
          group: ansblebaby
          wait: true
          region: "{{ region }}"
          count: 1  # default

          count_tag:
            Name: Demo
          instance_tags:
            Name: Demo
       register: ec2

```

### Run the Ansible Playbook :-

```
 ansible-playbook --syntax-check awcinstancecreation.yml
 ansible-playbook  awcinstancecreation.yml
``` 

### Sample Result

```bash

[ec2-user@ip-172-31-42-219 ~]$ ansible-playbook awcinstancecreation.yml

PLAY [creating aws instance by ansible code] ************************************************************************************************************************************************************************************************

TASK [creating ec2-instance] ****************************************************************************************************************************************************************************************************************
changed: [localhost]

PLAY RECAP **********************************************************************************************************************************************************************************************************************************
localhost                  : ok=1    changed=1    unreachable=0    failed=0
```

