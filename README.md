## Firstname : Olivier

## Surname : Djatchue-Tchokothe

## For Eazytraining's 18th DevOps Bootcamp

## Period : march-april-may

# Ansible Apache Installation Project

## Overview

This project automates the installation and configuration of an Apache server using Ansible. It includes setting up necessary prerequisites, configuring an Ansible role with a Jinja2 template, deploying an Apache container, and implementing security measures.

## Steps

1. **Prerequisites Installation**:
   - Install `python-pip`, `git`, and `epel-release` using pretasks.

2. **Role and Template Setup**:
   - Create an Ansible role to manage Apache installation and configuration.
   - Integrate a Jinja2 template file (`index.html.j2`) for the Apache default page.

3. **Apache Container Deployment**:
   - Deploy an Apache container and configure it to listen on port 82.

4. **Verification**:
   - Ensure the playbook runs successfully.
     >![playbook](https://github.com/user-attachments/assets/d0786f46-a7f0-4fea-a75e-7ff5f9fb18c2)

   - Verify the Apache container is running and listening on the specified port.
     >![docker_running](https://github.com/user-attachments/assets/0ed7df57-a5ce-49b7-9e21-a74cf5c6cf37)

   - Access the website to confirm it's serving the correct content.
     >![Website](https://github.com/user-attachments/assets/1eb567cd-b146-48e9-a215-c454d2d03488)


5. **Security**:
   - Encrypt Ansible passwords using `ansible-vault` and reference the encrypted file in the playbook.

## Summary

This project showcases the automation capabilities of Ansible for server configuration and deployment. Key learnings include role management, template integration, container deployment, and implementing security practices.

### Lessons Learned

- Effective management of Ansible roles.
- Integration of Jinja2 templates in Ansible roles.
- Deployment of Docker containers using Ansible.
- Importance of securing sensitive data with `ansible-vault`.

By completing this project, I have gained valuable skills in automating server setups and ensuring secure configurations using Ansible.
