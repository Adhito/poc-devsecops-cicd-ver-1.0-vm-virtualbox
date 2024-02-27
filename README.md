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
    **Note** :  Please replace $USER with your system's username, e.g., 'ubuntu'  
    **Note** : Once the installation complete do keep in mind to logout and login again in order for the changes to take effect  


- Testing You Docker With Sample Docker Containers:
    
    ```bash
    ## To Run The Container
    docker pull hello-world
    docker run -d --name devsecops-sample-hello-world -p 80:80 hello-world:latest
    
    ## To Stop & Delete The Container
    docker stop devsecops-sample-hello-world
    docker rm devsecops-sample-hello-world
    ```




<br><br><br>
### **Stage 2: Security Scanning For Code and Container Image**


**Sub-Stage 2.1: Setup & Install SonarQube (Docker & Docker-Compose):**
- Install SonarQube and Trivy on the VM instance to scan for vulnerabilities with Docker Standalone
        
    ```bash 
    ## Sonarqube Standalone
    docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
    ```
  
- Install SonarQube and Trivy on the VM instance to scan for vulnerabilities with Docker Compose
        
    ```bash 
    ## Sonarqube & PostgreSQL To Store Data
    docker-compose up $docker_compose_script 
    ```
    
- Once SonarQube is installed, you can access it on : 

        <VM-IP-adress>:9000 
  **Note** : If you install SonarQube with default settings then the default username & password is admin        


<br><br><br>
- [ ] TODO : Provide Detailed steps on adding current user to sudoers group at Sub-Stage 1.2
- [ ] TODO : Provide VM Formation / Architecture 
- [ ] TODO : Provide Detailed Docker Compose Script at Sub-Stage 2.1
- [ ] TODO :
- [ ] TODO :

