# Network automation using Ansible With Haproxy as Load Balancer

Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code. It runs on many Unix-like systems, and can configure both Unix-like systems as well as Microsoft  Windows.

ssh config example

```
Host bastionET2598
    Hostname publicIP
    user ubuntu
    IdentityFile ~/.ssh/yourKey
    ForwardAgent yes
    ControlMaster auto
    StrictHostKeyChecking no
    ControlPath ~/.ssh/ansible-%r@%h:%p
    ControlPersist 5m

Host devA
    Hostname 10.6.0.X
    user ubuntu
    IdentityFile ~/.ssh/yourKey
    StrictHostKeyChecking no
    ProxyCommand ssh -W %h:%p bastionET2598
  
Host devB
    Hostname 10.6.0.Y
    user ubuntu
    IdentityFile ~/.ssh/yourKey
    StrictHostKeyChecking no
    ProxyCommand ssh -W %h:%p bastionET2598
    
Host devC
    Hostname 10.6.0.Z
    user ubuntu
    IdentityFile ~/.ssh/yourKey
    StrictHostKeyChecking no
    ProxyCommand ssh -W %h:%p bastionET2598

Host devhaproxy
    Hostname 10.6.0.Q
    user ubuntu
    IdentityFile ~/.ssh/yourKey
    StrictHostKeyChecking no
    ProxyCommand ssh -W %h:%p bastionET2598
```
Run the playbook

```
ansible-playbook -i hosts site.yaml
```
