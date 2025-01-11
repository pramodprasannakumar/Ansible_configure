master:  ec2-user linux

yum install ansible -y
yum install python3-pip -y

in root do ssh-keygen

copy idrsa.pub to paste in slave user authorized key


in slave 

create user pramod
and passwd  devops12

inside user do ssh-keygen

copy idrsa.pub of master  to paste in slave user authorized key




in master :

cd /etc/ansible/

vi hosts


[project]
172.31.82.177 ansible_user=pramod ansible_become_password=devops12



cd roles

#do run galaxy inside roles only


 ansible-galaxy init java
  ansible-galaxy init git
  ansible-galaxy init jenkins
  ansible-galaxy init tomcat
  ansible-galaxy init maven



edit java role inside /tasks/main.yaml



---
- name: Install java
  ansible.builtin.yum:
    name: java-17-amazon-corretto-devel
    state: present
  become: yes





comeback to cd /etc/ansible

vi playbook.yaml


---
- name: Performing the task
  hosts: project
  roles:
    - java
   # - git
   # - tomcat
   # - jenkins
   # - maven
   # - nexus
   # - sonarqube
   # - gradle
   # - junit
  #  - k8s
 

run the below command to install it in slave machine


ansible-playbook playbook.yaml




extra:


ansible-playbook playbook.yaml --ask-become-pass

 ansible-playbook playbook.yaml --syntax-check










extra:-



vi ansible.cfg

[defaults]
remote_tmp = /tmp/.ansible/tmp
