# SYSTEM-Ansible-Ubuntu

by Nicolas MICHEL [@vpackets](https://twitter.com/vpackets) / [LinkedIn](https://www.linkedin.com/in/mclnicolas/) / [Blog](http://vpackets.net/) 

_**This disclaimer informs readers that the views, thoughts, and opinions expressed in this series of posts belong solely to the author, and not necessarily to the author’s employer, organization, committee or other group or individual.**_

## Description

Multiple playbooks that will perform basic function on Ubuntu (tested with 18.04.3 and 22.04 LTS) : Install package - Install Docker - Reboot and Update.

Git Repository: https://github.com/vPackets/ANSIBLE-Ubuntu-Manage

## Requirements
* Python (≥ 2.6)
* Ansible
* PyVmomi

## Configuration files:

```
├── Readme.md
├── hosts.ini
├── reboot.yml
├── ubuntu18.04
│   ├── README.md
│   ├── docker-stop-test-container.yaml
│   ├── docker-sudo.yaml
│   ├── install-docker.yaml
│   ├── install-package.yaml
│   ├── reboot.yaml
│   └── update.yaml
└── update_upgrade_playbook.yml
```

## Generalities

For this particular playbook I have copied my ssh keys to the remote server.

- Generate the ssh keys
```
ssh-keygen -t ed25519 -C "email@email.com"
```

- Copy the SSH keys to the remote servers

```
ssh-copy-id user@server
```

Also this repo contains an example of the hosts.ini configuration that could be used for this playbook. Make sure to rename the hosts-example.ini into hosts.ini and modify that file to reflect your servers IP address and credentials.

## Playbook execution:for ubuntu 22.04

### Step 1: Update Ubuntu on Ubuntu Virtual machines

This playbook will also upgrade containerlab

```
ansible-playbook -i hosts.ini update_upgrade_playbook.yml --ask-become-pass
```

### Step 2: Reboot

```
ansible-playbook -i hosts.ini reboot.yml --ask-become-pass 
```


## Playbook execution:for ubuntu 18.04

### Step 1: Update Ubuntu on Ubuntu Virtual machines

```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass update.yaml  
```

### Step 2: Reboot Ubuntu on Ubuntu Virtual machines

```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass reboot.yaml  
```

### Step 3: Install Package on Ubuntu Virtual machines

```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass install-package.yaml  
```

### Step 4: Install docker

```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass install-docker.yaml 
```

### Step 5: Add the Docker group to the user nmichel
 
```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass docker-sudo.yaml
```

### Step 6: Stop the test containers
 
```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass docker-stop-test-container.yaml
```

### Step 0: Deploy the complete solution

```
ansible-playbook -k --extra-vars "ansible_user=nmichel" --ask-become-pass complete-deployment.yaml
```


