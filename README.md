## ansible-aws-alb-tg 

This role create AWS target group with Application load balancer. You can enable support AWS Gather instance facts.

## Requirements
```sh
Ansible >= 2.5.0.0
boto3
Role Variables
```

main file which contains variables values

vars/main.yml:

```sh
---
###values of variables uses in ALB and TG###
aws_alb_tg_tg_name: test-target-group
aws_alb_tg_tg_ws_name: test-target-group-ws

aws_alb_tg_alb_name: test-alb-name
aws_alb_tg_region: us-east-1 
aws_alb_tg_instance_name: unicanova
aws_alb_tg_instance_env: dev
aws_alb_tg_security_groups: sg-1953db68
aws_alb_tg_vpcid: vpc-5f97633b
aws_alb_tg_alb_subnet_ids:
  - subnet-c1de9aea
  - subnet-7bfcac22
aws_alb_tg_alb_listeners:
  - Protocol: HTTPS
    Port: 443
    DefaultActions:
      - Type: forward
        TargetGroupName: "{{ aws_alb_tg_tg_name }}"
    Certificates:
      - CertificateArn: "arn:aws:acm:us-east-1:329942816198:certificate/338d2752-79c7-4cb6-a022-eb2f0d558704"
    SslPolicy: ELBSecurityPolicy-2015-05

aws_alb_tg_target_groups:
  - name: "{{ aws_alb_tg_tg_name }}"
  - name: "{{ aws_alb_tg_tg_ws_name }}"
    stickiness_enabled: True
subnets: - subnets for 
  - "subnet-3a0d4877"
  - "subnet-40b2993b"
```

---
#### Example Playbook
Export enviroment variables with AWS credentials:

```sh
$ export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
$ export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
```

Create dir when you clone ansible role from github:

```sh
$ mkdir -p example/roles
cd example
```

Clone role repository from github and configure ansible:

```sh
$ cd roles
$ git clone git@github.com:unicanova/unicanova/ansible-aws-alb-tg
$ cd ..
```
Edit ansible.cfg

```sh
[defaults]
hostfile = ./hosts.cfg
remote_user = constintine
host_key_checking = False
timeout = 5
pipelining = True
roles_path = .

Example playbook
- hosts: 127.0.0.1
  connection: local
  tasks:
    - name: Deploy AWS alb
      import_role:
        name: aws-alb-tg
```
Run anisble:

```sh
$ ansible-playbook site.yaml -t test
```
License
-------

MIT

Author Information
------------------
Author: Konstantin Kalinovskyi

Email: k@unicanova.com

Company: UnicaNova 

Website: https://unicanova.com/

