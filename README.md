# Modern End-to-End DevOps Pipeline

## Project Overview

This project demonstrates the implementation of an end-to-end DevOps pipeline for deploying two web applications to AWS EC2.

The project uses Infrastructure as Code, configuration management, containerization and Continuous Integration/Continuous Deployment (CI/CD) to automate application deployment.

The two applications deployed are:

1. A Portfolio Website built with HTML and CSS.
2. A Java Yearbook Application built using Java and Maven.

Both applications run on a single AWS EC2 instance using Docker and Docker Compose.

## Live Applications

| Application | URL |
|---|---|
| Portfolio Website | http://3.249.175.233 |
| Java Yearbook Application | http://3.249.175.233:8081 |

## Technologies Used

- AWS EC2 – Cloud hosting.
- Terraform – Infrastructure provisioning.
- Ansible – Server configuration and application deployment.
- Docker – Application containerization.
- Docker Compose – Managing multiple containers.
- Jenkins – CI/CD automation.
- Git and GitHub – Version control and source code management.
- Java – Backend application.
- Maven – Java build automation.
- HTML and CSS – Portfolio frontend.
- Linux – Server environment.

## Project Architecture

The deployment process follows this workflow:

1. Source code is stored in GitHub.
2. Jenkins retrieves the project from GitHub.
3. Maven builds the Java application.
4. Jenkins archives the generated Java artifact.
5. Jenkins connects to the AWS EC2 instance using SSH.
6. Application files are transferred to the EC2 server.
7. Docker Compose builds and starts the application containers.
8. Both applications become accessible through their respective public ports.

Terraform is used to provision the AWS infrastructure, while Ansible is used for server configuration and the initial application deployment.

## Infrastructure Provisioning – Terraform

Terraform provisions the AWS infrastructure required to host the applications.

The infrastructure includes:

- AWS VPC.
- Public subnet.
- Internet Gateway.
- Route table and route table association.
- Security group.
- EC2 instance.
- Public IP address.

The security group allows the required application and administration traffic.

| Port | Purpose |
|---|---|
| 22 | SSH access |
| 80 | Portfolio Website |
| 8081 | Java Application |

## Configuration Management – Ansible

Ansible is used to configure the EC2 instance and prepare it for application deployment.

The Ansible playbook performs tasks including:

- Updating system packages.
- Installing Docker.
- Starting the Docker service.
- Installing Docker Compose and Buildx.
- Transferring application files.
- Transferring the Docker Compose configuration.
- Building and starting the application containers.

## Containerization – Docker and Docker Compose

Both applications are containerized using Docker.

Separate Dockerfiles are maintained for the applications.

Docker Compose manages both services from a single configuration file.

| Container | Port |
|---|---|
| Portfolio Application | 80 |
| Java Yearbook Application | 8081 |

Both containers are configured to restart automatically unless stopped.

## CI/CD – Jenkins Pipeline

Jenkins automates the build and deployment process.

The pipeline is defined in the `jenkinsfile` located in the project root.

### Pipeline Stages

**1. Checkout**

Jenkins retrieves the latest source code from the GitHub repository.

**2. Build Java Application**

Maven compiles and packages the Java application.

**3. Archive Build**

The generated Java JAR artifact is archived in Jenkins.

**4. Deploy Applications**

Jenkins connects to the EC2 instance through SSH, transfers the application files and executes Docker Compose to rebuild and start the applications.

**5. Verify Deployment**

Jenkins checks both application endpoints to confirm that the applications are responding.

## Project Structure

```text
myprojectdevops2026/
│
├── ansible/
│   └── playbook.yml
│
├── java/
│   ├── Dockerfile
│   ├── pom.xml
│   └── src/
│
├── portfolio/
│   ├── Dockerfile
│   ├── index.html
│   └── style.css
│
├── terraform/
│   └── main.tf
│
├── docker-compose.yml
├── jenkinsfile
├── .gitignore
└── README.md
```

## Deployment Results

The project successfully demonstrates:

- Infrastructure provisioning with Terraform.
- EC2 configuration with Ansible.
- Docker image building and containerization.
- Running multiple applications using Docker Compose.
- Java application compilation using Maven.
- Automated deployment through Jenkins.
- Successful application availability through public EC2 endpoints.

The Jenkins pipeline completed successfully, including deployment and application verification.

## GitHub Repository

https://github.com/DNK93/myprojectdevops2026

## Conclusion

This project demonstrates how DevOps tools and practices can be integrated to automate infrastructure provisioning, configuration management, application building, containerization and deployment.

The final result is a working deployment of two applications on AWS EC2, supported by a Jenkins CI/CD pipeline.