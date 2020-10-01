# SYSTEM-Ansible-Ubuntu

by Nicolas MICHEL [@vpackets](https://twitter.com/vpackets) / [LinkedIn](https://www.linkedin.com/in/mclnicolas/) / [Blog](http://vpackets.net/) 

_**This disclaimer informs readers that the views, thoughts, and opinions expressed in this series of posts belong solely to the author, and not necessarily to the author’s employer, organization, committee or other group or individual.**_

## Description

Multiple playbooks that will perform basic function on Ubuntu (tested with 18.04.3) : Install package - Install Docker - Reboot and Update.

## Requirements
* Python (≥ 2.6)
* Ansible
* PyVmomi

## Configuration files:

```
├── README.md
├── complete-deployment.yaml
├── docker-stop-test-container.yaml
├── docker-sudo.yaml
├── install-docker.yaml
├── install-package.yaml
├── reboot.yaml
└── update.yaml
```

## Playbook execution:

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


