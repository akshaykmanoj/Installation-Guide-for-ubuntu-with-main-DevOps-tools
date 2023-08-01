# Installing WSL - Ubuntu, Jenkins, Docker, Minikube, Kubernetes, and Helm on Windows

This guide will walk you through the process of setting up a development environment on Windows, including Windows Subsystem for Linux (WSL) with Ubuntu, Docker, Minikube, Kubernetes, and Helm. These tools are commonly used for containerization and Kubernetes cluster management. It also includes a reference link for Istio installation.

## Prerequisites

- Windows 10 Pro, Enterprise, or Education (64-bit)
- Java Development Kit (JDK) 11 or higher
- At least 4GB of RAM and virtualization enabled in BIOS
- Reliable internet connection

## Steps

1. **Install Windows Subsystem for Linux (WSL)**

   Open PowerShell as an administrator and run the following command to enable WSL:
   
2. **Install Ubuntu from Microsoft Store**

   Open Microsoft Store, search for "Ubuntu," and install it.

   Launch Ubuntu, and you'll be prompted to set up a username and password for your Ubuntu environment.

3. **Install Jenkins**
   
     1. **Update Package Lists and Install Java Development Kit (JDK)**

        Open a terminal and run the following command to update the package lists and Install OpenJDK 11(Jenkins requires Java to run) on your system:
   
         - sudo apt update
         - sudo apt install -y openjdk-11-jdk
     
    2. **Add Jenkins Repository and Import the Repository Key**

       Run the following commands to add the Jenkins repository to your system and import the repository key:
         - wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
         - sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  
    3. **Install Jenkins**

       Run the following commands to install Jenkins:
  
         - sudo apt update
         - sudo apt install -y jenkins

    4. **Start Jenkins**

       After the installation, Jenkins should start automatically. However, you can use the following commands to start and check the status of Jenkins:
  
      - sudo systemctl start jenkins
      - sudo systemctl status jenkins

       If Jenkins is running correctly, the status command should display "active (running)".
   

    5. **Access Jenkins Web Interface**

       Jenkins runs on port 8080 by default. Open your web browser and navigate to:
  
         *http://localhost:8080/*

       If you are accessing Jenkins from a remote machine, replace "localhost" with your server's IP address or domain name.
       

    7. **Unlock Jenkins**

       When you first access the Jenkins web interface, you will be asked to unlock Jenkins. The initial admin password can be found on the server at:       
       /var/lib/jenkins/secrets/initialAdminPassword
    
       Use the following command to view the password:
          - sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    
       Copy the password and paste it into the web interface to unlock Jenkins.

    8. **Install Plugins**

       Jenkins will prompt you to install the recommended plugins. Proceed with the installation of suggested plugins or select the plugins you need.

    9. **Create Admin User**

       Set up the admin user with the required credentials.

    10. **Start Using Jenkins**

      Jenkins is now ready to use! You can start creating jobs and managing your CI/CD pipelines.

3. **Install Docker Desktop for Windows**

   Download Docker Desktop for Windows from the Docker website: [Docker Desktop](https://www.docker.com/products/docker-desktop)

   Run the installer and follow the on-screen instructions to install Docker Desktop.

   Verify the installation by running `docker --version` in the Command Prompt. Docker Desktop will act as the hypervisor backend for Minikube running within the Ubuntu       environment in WSL.

   > Note: Docker Desktop will manage the containers for Minikube, allowing you to run a Kubernetes cluster within your Ubuntu WSL environment while utilizing Docker's       capabilities on your Windows machine. This integration ensures seamless container management for Minikube.

4. **Install Minikube and Kubectl**

    1. Open the Ubuntu terminal and install kubectl, which is a command-line tool for interacting with Kubernetes:

    - sudo apt update
    - sudo apt install -y kubectl
  
    2.install minikube
   
    - curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    - chmod +x minikube-linux-amd64
    - sudo mv minikube-linux-amd64 /usr/local/bin/minikube

5. **Start Minikube**

   In the Ubuntu terminal, start Minikube using the docker driver (if you are using VirtualBox, set the driver as VirtualBox):

      - minikube start --driver=docker
  
      Verify installation by using the command `minikube status`. If Minikube is running correctly, you should see information about the Minikube cluster, such as the       Kubernetes version and control plane status.

6. **Install Helm**

   In the Ubuntu terminal, download and install Helm using the official script:
   - curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
   - chmod +x get_helm.sh
   - ./get_helm.sh
   Verify the Helm installation by running *helm version*.

   > For installing Istio, refer to: [Istio Getting Started Guide](https://istio.io/latest/docs/setup/getting-started/)
   

That's it! You now have a Kubernetes development environment with WSL, Ubuntu, Docker, Minikube, and Helm set up on your Windows machine. You can use this environment to develop and manage applications using containers and Kubernetes.

## Note

Please note that the steps provided in this guide are based on the information available at the time of creation and may be subject to change. Software versions, installation procedures, and dependencies might be updated by the respective projects.

For the most up-to-date and accurate information, always refer to the official documentation of each tool or project:

- [Windows Subsystem for Linux (WSL) Official Documentation](https://docs.microsoft.com/en-us/windows/wsl/)
- [Docker Desktop Official Documentation](https://docs.docker.com/products/docker-desktop/)
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Minikube Official Documentation](https://minikube.sigs.k8s.io/docs/)
- [Kubernetes Official Documentation](https://kubernetes.io/docs/home/)
- [Helm Official Documentation](https://helm.sh/docs/)

Before proceeding with the installation or troubleshooting, check the official documentation to ensure you have the latest information and avoid any potential errors.

If you encounter any issues or have questions regarding the setup, feel free to reach out to the respective communities or support channels for assistance.

You can reach me at nusairtech@gmail.com.

Happy Kubernetes development!






