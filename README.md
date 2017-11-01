# Ansible Sonarqube Config Example
Minimal Ansible SonarQube Configuration Example.

This will set a SonarQube instance Auth to true using uri, and also load a sample xml profile via curl.


## Force User Authentication

Jumping straight to the Ansible code the following modifies the forceAuthentication setting:

```
    - name: Force User Authentication
      uri:
        url: "{{ sonar_api_url }}/settings/set"
        method: POST
        status_code: 204
        body: "key=sonar.forceAuthentication&value=true"
        force_basic_auth: yes
        user: "{{ sonar_token }}"
        password: "{{ sonar_password }}"
        validate_certs: no
```

## SonarQube Profile

And the curl* command below loads in a profile:

```        
    - name: POST a SonarQube Profile xml via curl
      shell: 'curl  -X "POST" "{{ api_url }}/qualityprofiles/restore" \
                    -H "Content-Type: multipart/form-data; charset=utf-8; boundary=__X_PAW_BOUNDARY__" \
                    -u {{ username }}: \
                    -k \
                    --form backup=@{{ sonar_profile }}'
```
* Note: I tried to use uri: but couldn't locate the correct incantation.


## Requirements
Local installation of Ansible.

## Run

Copy your SonarQube profile into a file in this repo's root folder and name it ```SonarQubeProfile.xml```.

Call ansible-playbook command below:

```
ansible-playbook -i ./inventory.yml SonarQubeConfig.yml
```
