# Ansible playbook with shell to collect metrics - CPU, Memory and Diskspace from the worker nodes

## Launch EC2 Instances

Launch one Ansible master instance and 2 worker nodes. Here we are going to collect the system level metrics from worker node.

![image](https://github.com/kohlidevops/anisble-shell-collect-system-metrics/assets/100069489/2638bfea-1cdc-4675-9d9b-0d804b716286)

## Ansible Master node

SSH to Ansible master instance and install below commands to make ansible master.

```
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
ansible --version
```

### Generate SSH Key

To generate SSH-Keygen in ansible master using below commands

```
ssh-keygen
cat /home/ubuntu/.ssh/id_rsa.pub
```

#### To Copy the public key and use later

## Ansible worker nodes

SSH to both worker nodes and perform below commands

```
$sudo apt-get update -y
$ssh-keygen
$sudo vi /home/ubuntu/.ssh/authorized_keys
```
Paste the Ansible master public key and save to grant permission to access the worker nodes from master node.

## Ansible Master node

Try to access the bothe worker nodes from master node using below command

```
ssh ec2-instance-private-ip
```

## Configure Inventory in Ansible master node

```
sudo nano /etc/ansible/hosts

add below lines in to the hosts file

[monitoring]
10.10.10.1
10.10.10.2

save and exit
```

### To access the worker node

```
ansible monitoring -m ping
```

![image](https://github.com/kohlidevops/anisble-shell-collect-system-metrics/assets/100069489/8c869b8f-d029-4c23-b40d-0e57bedcfeb3)

### Create a Playbook to collect the system metrics

```
sudo nano monitor.yml

You can access the below link to copy paste the yaml file
```

### To check the syntax 

```
ansible-playbook monitor.yml --syntax-check
```

### To run the playbook

```
ansible-playbook monitor.yml
```

![image](https://github.com/kohlidevops/anisble-shell-collect-system-metrics/assets/100069489/aa3d1e2c-6fd5-4a38-8813-d7cffaa4ef9d)

That's it!
