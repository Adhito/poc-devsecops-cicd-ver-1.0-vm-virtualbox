# Project DevSecOps CICD Version 1.0 VM on Local (VirtualBox)


### **Stage 1: Setup the CICD Pipeline with Jenkins (DEVCICDJENKINS01)**

**Sub-Stage 1.1: Create New VM in Virtual Box (Ubuntu 22.04):**

- Setup the NAT networks on the Virtual Box so that the VM(s)can communicate with each other.
- Provision a new VM (DEVCICDJENKINS01) with Ubuntu 22.04.
- If guest mode if checked on the virtualbox then you don't need to input all the credential (user, timezone & etc) since it will be automatically created.

**Sub-Stage 1.2: Setup & Update the VM:**

- Once the installation is complete ensure the VM is up to date
    
    ```bash
    sudo apt-get update
    ```
- Add the current user to the sudoers group, otherwise you wont be able to install various library


- [ ] TODO : Provide detailed steps on adding current user to sudoers group at Sub-Stage 1.2
- [ ] TODO : Provide VM Formation / Architecture 
- [ ] TODO :
- [ ] TODO :

