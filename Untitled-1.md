Capstone Project Instructions : Modern End-to-End DevOps Pipeline

Project Objective :
Design and implement a fully automated DevOps pipeline to provision cloud infrastructure and deploy two distinct applications on the same server using Infrastructure as Code (IaC), Containerization, Configuration Management, and CI/CD automation.
------------------------------
Project Tech Stack
You should implement your solution using this toolchain:

* Version Control: GitHub - github.com/ProfAkymbo/java-yearbook-project
* Cloud Provider: Amazon Web Services (AWS)
* Infrastructure as Code: Terraform
* Configuration Management: Ansible
* Containerization: Docker & Docker Compose
* CI/CD Tool : Jenkins or GitHub Actions
------------------------------
Step-by-Step Instructions
Step 1: Prepare the Applications

   1. Portfolio Web App:
   * Create a simple personal portfolio website (index.html) using HTML/CSS.
      * Containerize it
   2. Java Application:
   * Use the source code from this project repo above.
      * Also containerize it.

Step 2: Define Infrastructure with Terraform
Navigate to the terraform/ directory and write configuration files to provision:

* A custom AWS VPC with an Internet Gateway and a Public Subnet.
* An AWS EC2 Instance
* A Security Group opening ingress traffic for:
* Port 22 (SSH management)
   * Port 80 (Portfolio App)
   * Port 8081 (Java App)

Step 3: Configure and Deploy with Ansible & Docker
Inside the ansible/ directory, develop a configuration management plan:

   1. Docker Compose: Write a docker-compose.yml that builds and mounts both apps:
      Map the Portfolio Web App container to host port 80.
      Map the Java Application container to host port 8081.
   2. Ansible Playbook: Write a playbook.yml that targets your EC2 server to:
       Install system dependencies, Docker, and Docker Compose.
      Transfer your deployment configurations and source files to the target instance.
      Execute docker compose up -d --build to deploy both containers.

Step 4: Automate the CI/CD Pipeline
Using Jenkins or GitHub Actions :

   1. Checkout Code: Pull your latest code onto the GitHub runner.
   2. Java Build: Compile and package the Java application using Maven/Gradle.
   3. Terraform Lifecycle: Initialize and apply the Terraform configuration using securely injected AWS Secrets.
   4. Inventory Generation: Capture the generated EC2 Public IP from the Terraform output and dynamically write it to Ansible's inventory.ini.
   5. Ansible Execution: Run the Ansible playbook against the live server to finish configuration and launch your applications.

------------------------------
Expected Deliverables
Upon completion, you must submit:

   1. GitHub Repository Link: Containing your source files, IaC , playbooks, and pipeline configurations.
   2. Functional App URLs: Accessible public browser endpoints demonstrating your deployment:
   http://<YOUR-EC2-PUBLIC-IP>:80 — Portfolio Web Application
      http://<YOUR-EC2-PUBLIC-IP>:8081 — Java Application
   3. README.md File: Clear setup instructions detailing how you configured everything.