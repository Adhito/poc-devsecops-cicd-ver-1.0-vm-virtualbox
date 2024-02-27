# Project DevSecOps CICD Version 1.0 VM on Local (VirtualBox)


### **Stage 1: Setup the CICD Pipeline with Jenkins (DEVCICDJENKINS01)**


**Sub-Stage 1.1: Create New VM in Virtual Box (Ubuntu 22.04):**

- Setup the NAT networks on the Virtual Box so that the VM(s)can communicate with each other.
- Provision a new VM (DEVCICDJENKINS01) with Ubuntu 22.04.
- If guest mode if checked on the virtualbox then you don't need to input all the credential (user, timezone & etc) since it will be automatically created.


**Sub-Stage 1.2: Setup & Update the VM Latest Security Patch:**

- Once the installation is complete ensure the VM is up to date
    
    ```bash
    sudo apt-get update
    ```
- Add the current user to the sudoers group, otherwise you wont be able to install various library


**Sub-Stage 1.3: Setup & Install Container Engine (Docker):**

- Set up Docker on the DEVCICDJENKINS01 VM:
    
    ```bash
    
    sudo apt-get update
    sudo apt-get install docker.io -y
    sudo usermod -a -G docker $USER
    newgrp docker
    ```
    N.B :  Please replace $USER with your system's username, e.g., 'ubuntu'

    Once the installation complete do keep in mind to logout and login again in order for the changes to take effect

    

- [ ] TODO : Provide detailed steps on adding current user to sudoers group at Sub-Stage 1.2
- [ ] TODO : Provide VM Formation / Architecture 
- [ ] TODO :
- [ ] TODO :

