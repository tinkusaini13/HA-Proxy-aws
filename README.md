# HA-Proxy-aws

setup HA-Proxy required aws ec2-intance private key (( web.pem )) and main  playbook is master.yml 

ansible-playbook master.yml -i inventory --private-key="web.pem"

http://13.233.76.19:8080/
