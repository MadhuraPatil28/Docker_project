EMart Microservices: Containerized Architecture
This repository contains the containerized deployment of the EMart Application, a multi-tier microservices project. It leverages Docker and Docker Compose to orchestrate a frontend, multiple backend APIs, and both SQL and NoSQL databases.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fce06cbe-88fc-497e-b8dc-87fabba4883c" />

Architecture Overview
The application is split into five main services:
Client (Angular): The frontend UI serving on port 4200.
API (Node.js): Backend service handling core EMart logic on port 5000.
WebAPI (Java/Spring Boot): Specialized service for book data on port 9000.
NGINX Gateway: Acts as a Reverse Proxy, routing traffic to the appropriate service.
Databases: * MongoDB: NoSQL storage for the Node.js API.
MySQL: Relational storage for the Java API.

Gemini said
Since you have both the Dockerfiles and the Docker Compose configuration, your README should focus on how these components work together to create a microservices ecosystem.

Here is a structured template you can copy and paste into your README.md.

EMart Microservices: Containerized Architecture
This repository contains the containerized deployment of the EMart Application, a multi-tier microservices project. It leverages Docker and Docker Compose to orchestrate a frontend, multiple backend APIs, and both SQL and NoSQL databases.

🏗 Architecture Overview
The application is split into five main services:

Client (Angular): The frontend UI serving on port 4200.

API (Node.js): Backend service handling core EMart logic on port 5000.

WebAPI (Java/Spring Boot): Specialized service for book data on port 9000.

NGINX Gateway: Acts as a Reverse Proxy, routing traffic to the appropriate service.

Databases: * MongoDB: NoSQL storage for the Node.js API.

MySQL: Relational storage for the Java API.

Project Structure:
├── client/          # Angular Frontend source & Dockerfile
├── nodeapi/         # Node.js API source & Dockerfile
├── javaapi/         # Java Spring Boot source & Dockerfile
├── nginx/           # NGINX configuration (default.conf)
└── docker-compose.yml

🚀 Getting Started
Prerequisites
Docker (v20.10+)
Docker Compose (v1.29+)

Deployment on AWS EC2:
1. Instance Requirements
AMI: Ubuntu 24.04 LTS
Type: t3.medium (minimum 4GB RAM required for Java/Maven builds).
Storage: 20GB EBS Volume.

Gemini said
For deploying your EMart project on AWS EC2, here is the most efficient, "copy-paste" ready guide to include in your README. This covers the transition from your local Docker setup to a live cloud instance.

☁️ Deployment on AWS EC2
Deploying to EC2 allows your microservices to be accessible over the public internet rather than just localhost.

1. Instance Requirements
AMI: Ubuntu 24.04 LTS

Type: t3.medium (minimum 4GB RAM required for Java/Maven builds).

Storage: 20GB EBS Volume.

2. Security Group Configuration
Ensure your EC2 Security Group has the following Inbound Rules:
Protocol	Port Range	Source	Description
SSH	22	My IP	Remote Access
HTTP	80	0.0.0.0/0	NGINX Gateway (Main Entry)
Custom TCP	4200	0.0.0.0/0	Angular Frontend
Custom TCP	5000	0.0.0.0/0	Node.js API
Custom TCP	9000	0.0.0.0/0	Java AP

3. Installation Script
Once you SSH into your instance (ssh -i key.pem ubuntu@public-ip), run this one-liner to set up the environment:
# Update and install Docker + Docker Compose
sudo apt update && sudo apt install -y docker.io
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Fix permissions (Log out and back in after this)
sudo usermod -aG docker $USER

4. Launching the App
   git clone <your-repo-url>
cd <project-dir>

# Build and start all 6 containers in the background
docker-compose up -d --build

5. Verification
Access your application using the EC2 Public IP:
Web UI: http://<EC2-Public-IP>:80
API Health: http://<EC2-Public-IP>:5000/api
