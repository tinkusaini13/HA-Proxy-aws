# HA-Proxy-aws

Deploying Load Balancer Using HAProxy and Multiple Webservers on AWS Instances Through Ansible

Load Balancer:

A load balancer acts as the “traffic cop” sitting in front of your servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximizes speed and capacity utilization and ensures that no one server is overworked, which could degrade performance. If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it.

HAProxy: 

HAProxy (High Availability Proxy) is an open source, fast, and reliable solution that provides load balancer and reverse proxy features for TCP- and HTTP-based applications. HAProxy load balancer handles heavy load traffic and reroutes requests seamlessly across multiple servers. 

HAProxy also supports the following features:

Layer 4 (TCP) and Layer 7 (HTTP) load balancing.
URL rewriting.
Health checks.
Proxying protocols.
HTTP message logging.
Rate limiting.
SSL/TLS termination.
Gzip compression.

Architcture of HA proxy

![image](https://user-images.githubusercontent.com/88707521/156538584-357f05af-4405-47a7-8ee5-ba701967437e.png)


Prerequisite:

  1. Ansible should be Installed in the atleast one system
  2. Basic Knowledge of AWS cloud

create a ec2-instance and install ansible 

 1. yum install -y python39
 2. pip3 install ansible --user
 
 
 create a inventory and ansible.cfg file:
 
 https://github.com/tinkusaini13/HA-Proxy-aws/blob/main/inventory
 
 ![image](https://user-images.githubusercontent.com/88707521/156539575-e8019117-f8b1-4b15-be9e-186e06d74f4f.png)

ansible.cfg file :

 https://github.com/tinkusaini13/HA-Proxy-aws/blob/main/ansible.cfg

![image](https://user-images.githubusercontent.com/88707521/156539770-528f2ed5-a018-4db5-b499-2052f2cda867.png)

check connectivity with node 

ansible all -m ping -i inventory --private-key="web.pem" 

![image](https://user-images.githubusercontent.com/88707521/156540818-b8aa2dea-912d-4c71-9893-48678a56ec92.png)


create a index.html file 

https://github.com/tinkusaini13/HA-Proxy-aws/blob/main/index.php

![image](https://user-images.githubusercontent.com/88707521/156541256-e7095d0a-0f7b-4362-9adb-058be4da924e.png)

configure the  HA-proxy configuration file 

Link here: https://github.com/tinkusaini13/HA-Proxy-aws/blob/main/haproxy.cfg

![image](https://user-images.githubusercontent.com/88707521/156541972-ca716381-3bd4-4ff7-af21-d5799c42e9b1.png)


Create main playbook of Setup HA-Proxy And httpd webserver :

link for main.yml: 

HA-proxy yml file :

![image](https://user-images.githubusercontent.com/88707521/156542431-289cfa0c-25a6-4f0d-abb7-0eda26b50da9.png)

httpd yml file: 

![image](https://user-images.githubusercontent.com/88707521/156542800-70c8bfce-3862-4c96-9dde-35dbef146842.png)

All configuration is completed run main.yml  playbook

Required file before run main playbook:

1. aws ec2-intance private key (( web.pem ))
2. inventory
3. ansible.cfg

How to run main.yml playbook:

ansible-playbook  master.yml  -i inventory --private-key="web.pem"

http://ip-HA-proxy:8080/

http://13.233.76.19:8080/

Refresh Browser see every time change the ip address.

Thank you





