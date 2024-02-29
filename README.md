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
- Install SonarQube on the VM instance to scan for vulnerabilities with Docker Standalone
        
    ```bash 
    ## Sonarqube Standalone
    docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
    ```
  
- Install SonarQube on the VM instance to scan for vulnerabilities with Docker Compose
        
    ```bash 
    ## Sonarqube & PostgreSQL To Store Data
    docker-compose up $docker_compose_script 
    ```
    
- Once SonarQube is installed, you can access it on : 

        <VM-IP-adress>:9000 
  **Note** : If you install SonarQube with default settings then the default username & password is admin        


**Sub-Stage 2.2: Setup & Install Trivy (Docker & Apt Install):**
- Install Trivy on the VM instance to scan for vulnerabilities with Docker Standalone
        
    ```bash 
    ## Trivy Docker
    $ docker command here
    ```
- Install Trivy on the VM instance to scan for vulnerabilities with APT install
        
    ```bash 
    ## Trivy Standalone
    sudo apt-get install wget apt-transport-https gnupg lsb-release
    wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
    echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
    sudo apt-get update
    sudo apt-get install trivy    
    ```
    
  To scan image using trivy
    ```
    trivy image <container_imageid>
    ```




<br><br><br>
### **Stage 3: Continous Integration and Continous Deployment (CI/CD) Setup**

**Sub-Stage 3.1: Setup & Install Jenkins:**

- Install Java Version 17 / 21
    ```bash
    sudo apt update
    sudo apt install fontconfig openjdk-17-jre
    java -version
    openjdk version "17.0.8" 2023-07-18
    OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
    OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
    ```


- Install Jenkins on the DEVCICDJENKINS01 VM instance to enable automatic deployment :
    ```bash
    #jenkins
    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins
    sudo systemctl start jenkins
    sudo systemctl enable jenkins
    ```
    
- Access Jenkins in a web browser using the NAT IP of your DEVCICDJENKINS01 VM instance.
    ```
    nat_ip_adress:8080
    ```

<br>
**Sub-Stage 3.2: Setup & Install Necessary Plugins:**
<br>
Login To Your Jenkins → Manage Jenkins → Plugins → Available Plugins →
<br>
Select The Following Plugins :

- Eclipse Temurin Installer (Install without restart)
- Email Extension Plugin
- NodeJs Plugin (Install Without restart)
- SonarQube Scanner (Install without restart)




<br><br><br>
- [ ] TODO : Provide Detailed steps on adding current user to sudoers group at Sub-Stage 1.2
- [ ] TODO : Provide VM Formation / Architecture 
- [ ] TODO : Provide Detailed Docker Compose Script at Sub-Stage 2.1
- [ ] TODO : Research on using Trivy with Container Engine (Docker/Podman) instead of local installation
- [ ] TODO :

