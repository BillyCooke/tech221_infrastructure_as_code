# Infrastrcuture as code (IaC)

## What is IaC?
Infrastructure as Code is the provisioning of infrastructure through code instead of through manual processes. You are able to create configuration files with infrastructure specification.

## What are the benefits?
* Consistent configurations
* Reduced risk - developing and deploying code multiple times can increase the risk of human error
* Faster deployment - use a single command only
* Cost saving
* Repeatable

## Use cases
* Provisioning
* Testing
* Security

## Who uses it?
Companies such as Amaozn and NEtflix use IaC to manage complex and to reduce the time that is put into develping and deploying code over and over again.

## What is configuration management?
It is the process of maintaining computer systems, servers and software in a consistent state. It is a way to ensure that a system runs as expected to as changes are made over time.

## What is Ansible?
Ansible is a powerful open-source automation software application which is written in Python. Is configures systems, deploys software and supports system updates. It can control as many nodes as needed (virtual machines).

## Benefits of Ansible
* Easy to learn
* Uses Python
* Playbooks are written in YAML
* No agent installations are required to manage nodes

## Ansible dependancies
* Python 2.7 - 3.6
* Ubuntu 18.04

## Ansible use cases
* Provisioning
* Configuration management
* Application deployment
* Continuous delivery

## What is YAML? (Yet Another Markup Language)
YAML is a programming language that is designed to be easily readable and it is often used to write configuration files.

## What are Playbooks?
It is a file that contains the ordered tasks that should be executed on a remote server to complete a task. It is essentially a to-do list for Ansible.

## Creating Ansible controller and Web and DB nodes
1. First we needed to open VS and make a new project
2. Open up a git bash terminal and use ```vagrant init``` to open up a vagrant file
3. Replace the code that is in there with the following code
```
# ansible-tech201


# -*- mode: ruby -*-
 # vi: set ft=ruby :
 
 # All Vagrant configuration is done below. The "2" in Vagrant.configure
 # configures the configuration version (we support older styles for
 # backwards compatibility). Please don't change it unless you know what
 
 # MULTI SERVER/VMs environment 
 #
 Vagrant.configure("2") do |config|
  # creating are Ansible controller
    config.vm.define "controller" do |controller|
      
     controller.vm.box = "bento/ubuntu-18.04"
     
     controller.vm.hostname = 'controller'
     
     controller.vm.network :private_network, ip: "192.168.33.12"
     
     # config.hostsupdater.aliases = ["development.controller"] 
     
    end 
  # creating first VM called web  
    config.vm.define "web" do |web|
      
      web.vm.box = "bento/ubuntu-18.04"
     # downloading ubuntu 18.04 image
  
      web.vm.hostname = 'web'
      # assigning host name to the VM
      
      web.vm.network :private_network, ip: "192.168.33.10"
      #   assigning private IP
      
      #config.hostsupdater.aliases = ["development.web"]
      # creating a link called development.web so we can access web page with this link instread of an IP   
          
    end
    
  # creating second VM called db
    config.vm.define "db" do |db|
      
      db.vm.box = "bento/ubuntu-18.04"
      
      db.vm.hostname = 'db'
      
      db.vm.network :private_network, ip: "192.168.33.11"
      
      #config.hostsupdater.aliases = ["development.db"]     
    end
  
  
  end
  ```
  4. Then use vagrant up in your terminal and it will begin to launch three different virtual machines. Controller, web and DB
  5. We need to open up three different Git Bash terminals and cd into the folder that you amde your prject in
  6. Then SSH into each virtual machine using vagrant ssh and then the name of the VM. For example ```vagrant ssh controller```
  7. In each terminal we want to run ```sudo apt update -y``` and ```sudo apt upgrade -y```
  8. Once your controller VM is running we need to make sure that it has the correct version of Python by using ```python --version```
  9. Anything between 2.7 to 3.6 is good and if it is below 2.7 you will need to install a later version
  10. Now we need to install ansible using the following
  ```
  sudo apt install software-properties-common
  sudo apt-add-repository ppa:ansible/ansible
  sudo apt update -y
  sudo apt install ansible -y
  ```
  11. Then use ```ansible --version``` to check you have the correct version
  12. we can then use ssh vagrant@'IP of VM' to take control of that VM through the controller VM. Answer yes when prompted and then if it asks for a password enter ```vagrant```. The password is invisible