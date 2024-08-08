## Firstname : Olivier

## Surname : Djatchue-Tchokothe

## For Eazytraining's 18th DevOps Bootcamp

## Period : march-april-may

# Ansible Apache Installation Project

## Summary

This project demonstrates the use of Ansible to automate the installation and configuration of an Apache web server on a remote server. The automation process is divided into two roles: `pretasks` and `install_apache`. The `pretasks` role installs necessary prerequisites, while the `install_apache` role sets up and starts the Apache container. For enhanced security, sensitive credentials are encrypted using Ansible Vault.

## Project Struckture
![projeckt structure](https://github.com/user-attachments/assets/3786999b-6b7e-47fd-a58b-b3456fdaf70f)

### Prerequisites

-   Ansible installed on the local machine.
-   A remote server with SSH access and docker allready installed.
-   Encrypted Ansible Vault for secure credential management.

### Roles and Tasks

#### 1. `pretasks` Role

This role ensures all necessary prerequisites are installed on the remote server. It includes:

-   Installation of `python-pip`.
-   Installation of `git`.
-   Enabling the EPEL repository for additional packages.

#### 2. `install_apache` Role

This role is responsible for configuring and starting the Apache web server. It includes:

-   Copying the Apache configuration template to the server.
-   Starting the Apache container to serve the website.

### Playbook Execution

The playbook is executed to run the above roles in sequence, ensuring the Apache web server is set up correctly.

## Steps to Execute the Project

1.  **Setup Ansible Inventory and Configuration:** Ensure your inventory file lists the target remote server(s) and your `ansible.cfg` is correctly configured.
    
2.  **Create Encrypted Credentials:** Encrypt the Ansible password using Ansible Vault:
    
    Save the encrypted password in a credential file and reference the path in your playbook.
    
3.  **Define Roles:**
    

**`pretasks`:**
  
```bash
    
       - name: Install EPEL repo
   package:
     name: "{{ item }}"
     state: present
   when: ansible_distribution == "CentOS"
   loop:
    - epel-release
    - git
    - wget

 - name: Download pip script
   get_url:
     url: https://bootstrap.pypa.io/pip/2.7/get-pip.py
     dest: /tmp/get-pip.py

 - name: Install python-pip
   ansible.builtin.command: python2.7 /tmp/get-pip.py

 - name: Install docker python
   pip:
     name: docker-py
   ````
**`Install_apache`:**
        
  
        
```bash

  - name: Copy website file template
  template:
    src: index.html.j2
    dest: "/home/{{ system_user }}/index.html"

- name: Create Apache container
  docker_container:
    name: webapp
    image: httpd
    ports:
      - "82:80"
    volumes:
      - "/home/{{ system_user }}/index.html:/usr/local/apache2/htdocs/index.html"
```
        
4.  **Run the Playbook:** Execute the playbook to apply the roles and tasks:
    
    ```bash 
    ansible-playbook -i prod.yml deploy.yml --ask-vault-pass` 
    ```
    
5.  **Verification:**
    
    -   Check that the playbook ran successfully using the provided screenshots.
  >![playbook](https://github.com/user-attachments/assets/d0786f46-a7f0-4fea-a75e-7ff5f9fb18c2)
    -   Verify the Apache container is running and listening on port 82.
   >![docker_running](https://github.com/user-attachments/assets/0ed7df57-a5ce-49b7-9e21-a74cf5c6cf37)

    -   Access the website and ensure it is served correctly.
 >![Website](https://github.com/user-attachments/assets/1eb567cd-b146-48e9-a215-c454d2d03488)

## Learning Outcomes

-   **Ansible Role Creation:** Understanding the structure and purpose of Ansible roles to modularize the automation tasks.
-   **Task Automation:** Automating the installation and configuration processes, reducing manual intervention and errors.
-   **Security Practices:** Implementing secure handling of sensitive information using Ansible Vault.
-   **Configuration Management:** Managing server configurations using templates for consistent and repeatable setups.
-   **Service Management:** Automating service management with Ansible to ensure services are running as expected.

## Conclusion

This project showcases the efficient use of Ansible for automating the setup of an Apache web server. By breaking down the tasks into roles, we achieved a clean and maintainable automation process. The inclusion of security practices with Ansible Vault ensures sensitive data is protected, highlighting the importance of secure automation.
