# ci/cd pipeline still in progress....

## Pre-requisite Knowledge
- Proficient in Ansible
- Proficient in Jenkins
- Knowledge of CI/CD Workflow

**Automating Jenkins and Sonarqube Set-up with Ansible**

- Servers to be provisioned should have the following requirements: 
        - atleast 4GB RAM
        - atleast 15 GB Disk Space

- Configure SSH Agent on Bastion Server(CI Server). Research on SSH Agent if not clear

- Install Ansible version 2.10 or above on Bastion Server

- Write ansible playbooks to install and configure other necessary softwares for the CI environment e.g Jenkins, etc.

*Note*: Check Jenkins and Sonarqube Documentations on how to install manually.
Note down the steps and automate with Ansible.

**Plugins Installed in Jenkins**
-	Blue Ocean
-	Bitbucket
-	Ansible
-	Maven (pre-installed in Jenkins)
-	Git (pre-installed in Jenkins)
-	Sonarqube
-	Junit (preinstalled in Jenkins)
-       Docker
-       Cloudbees Docker build and Push
-       Grype Scanner(Anchore is deprecated)
-       Kubernetes
-       Http Request
-       Pipeline Utility Steps

**Credentials to create in Jenkins**
-   bitbucket credentials
-   ssh credentials
-   sonarqube token
-   dockerhub login credentials





