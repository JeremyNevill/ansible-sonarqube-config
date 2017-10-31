# Ansible Sonarqube Config Example
Minimal Ansible SonarQube Configuration Example.

This will set a SonarQube instance Auth to true using uri, and also load a sample xml profile via curl.

## Requirements
Local installation of Ansible.

## Run

Copy your SonarQube profile into a file in this repo's root folder and name it ```SonarQubeProfile.xml```.

Call ansible-playbook command below:

```
ansible-playbook -i ./inventory.yml SonarQubeConfig.yml
```
