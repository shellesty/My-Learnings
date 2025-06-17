# EC2 DevOps Setup and Learning Summary

## Objective
I deployed a full-stack containerized application on an AWS EC2 instance, installed key DevOps tools (Docker, kubectl, Terraform), and enabled public access through proper security group configuration. This exercise gave me hands-on experience with cloud provisioning, container orchestration, and infrastructure preparation for automation.

## Tools Installed and Their Purpose

### 1. Docker
`Docker` is used for containerizing applications, making them portable and environment-independent.  
- Installed Docker Engine and Docker Compose.
- Verified the installation with `docker run hello-world`.
- Used `docker compose up -d` to run a multi-container application stack.

### 2. kubectl
`kubectl` is the CLI tool for interacting with Kubernetes clusters. It's essential for managing deployments, pods, and other Kubernetes resources.  
- Installed the latest version of `kubectl`.
- Verified it using `kubectl version`.

### 3. Terraform
`Terraform` enables Infrastructure as Code (IaC), allowing repeatable and version-controlled infrastructure provisioning.  
- Added the official HashiCorp repository and GPG key.
- Installed and verified Terraform using `terraform --version`.

## Application Deployment Process

Connected to and Prepared the EC2 Instance
- Launched an EC2 instance (**t3.large**) running Ubuntu.
- Connected using SSH and a `.pem` key.
- The default 8 GB volume was expanded to **30 GB** using:
  - `growpart` to resize the partition
  - `resize2fs` to expand the filesystem
- Verified the expansion using `df -h` and `lsblk`.

Cloned the Project Repository
- Cloned the `ultimate-devops-project-demo` repository from GitHub.
- Reviewed `.env` and `docker-compose.yml` files to understand port mappings and service behavior.

Ran the Application
- Launched all services using:
  ```bash
  docker compose up -d
  
Configured Network Access

- Modified the EC2 Security Group to allow inbound traffic on port 8080.
- Verified that the frontend service was mapped correctly to this port.

Accessed the Application

- Opened the application in a browser using: http://<EC2-Public-IP>:8080(port)

### Key Learnings

- Tools like Docker, kubectl, and Terraform must be installed directly inside the EC2 instance to manage applications and infrastructure.
- Docker Compose simplifies deployment of multi-service applications.
- Security Groups in AWS act as cloud firewalls and must be configured to expose application ports.
- EC2 root volumes can be resized dynamically using standard Linux tools without downtime.
- Reviewing and modifying `.env` and `docker-compose.yml` files is crucial to understand service architecture.
- This setup lays the foundation for advanced topics like Kubernetes deployment, infrastructure automation, and CI/CD.

### Outcome

By the end of this session, I had:

- Set up and configured an EC2 Ubuntu instance (t3.large) with a 30 GB root volume
- Installed and verified Docker, kubectl, and Terraform
- Deployed a containerized full-stack demo application using Docker Compose
- Configured the instance's security group for public access
- Accessed the running application from a web browser using the EC2's public IP and exposed port
- Built a foundational DevOps environment ready for further automation and orchestration
