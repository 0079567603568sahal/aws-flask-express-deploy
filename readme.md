🚀 AWS Flask + Express Fullstack Deployment (Task 1–3)

This project demonstrates a complete real-world production deployment pipeline for a full-stack application consisting of:

🧠 Flask (Python) backend API

⚡ Express (Node.js) frontend

🐳 Docker & Docker Compose for containerization

☁️ AWS EC2 for manual deployment

📦 AWS ECR + ECS + VPC for production-grade, serverless deployment

It’s a full DevOps lifecycle from local development → Dockerized services → cloud-native deployment.

📁 Project Structure
aws-flask-express-deploy/
├── Backend/
│   ├── app.py
│   ├── Dockerfile
│   └── requirements.txt
├── Frontend/
│   ├── index.js
│   ├── server.js
│   ├── package.json
│   ├── Dockerfile
│   └── docker-compose.yml
├── docker-compose.yml         # Combined deployment file (local/dev)
└── README.md                  # Project documentation

🧠 Overview of Tasks
Task	Description	Outcome
Task 1	Local Docker Compose deployment	Flask + Express run locally with Docker
Task 2	Deploy backend & frontend on separate EC2 instances	Fullstack app deployed on public IP
Task 3	Push Docker images to ECR, deploy via ECS + VPC	Production-grade deployment with scaling & networking
🐳 Task 1 – Local Deployment with Docker Compose
🔧 1. Clone and Build Containers
git clone https://github.com/yourusername/aws-flask-express-deploy.git
cd aws-flask-express-deploy
docker-compose up --build

✅ Verify Locally

Backend: http://localhost:5000

Frontend: http://localhost:3000

curl http://localhost:5000
# {"message": "Hello from Flask backend!"}

☁️ Task 2 – Deploy on AWS EC2
🔐 1. Launch Two EC2 Instances

backend-server – Flask backend

frontend-server – Express frontend

Install Docker + Git:

sudo apt update -y
sudo apt install docker.io docker-compose -y

📦 2. Clone Repo & Run Containers on Each Instance

Backend EC2:

git clone https://github.com/yourusername/aws-flask-express-deploy.git
cd aws-flask-express-deploy/Backend
sudo docker-compose up -d --build


Frontend EC2:

cd aws-flask-express-deploy/Frontend
sudo docker-compose up -d --build


✅ Verify Deployment:

Backend: http://<EC2_PUBLIC_IP_BACKEND>:5000

Frontend: http://<EC2_PUBLIC_IP_FRONTEND>:3000

☁️ Task 3 – Production Deployment with ECR + ECS + VPC
🛠️ 1. Authenticate Docker to ECR
aws ecr get-login-password --region ap-southeast-2 \
| docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com

🐳 2. Build, Tag, and Push Images
# Backend
cd Backend
docker build -t flask-backend .
docker tag flask-backend:latest <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/flask-backend:latest
docker push <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/flask-backend:latest

# Frontend
cd ../Frontend
docker build -t express-frontend .
docker tag express-frontend:latest <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/express-frontend:latest
docker push <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/express-frontend:latest


✅ Verify:

aws ecr describe-images --repository-name flask-backend --region ap-southeast-2

🛳️ 3. Create ECS Cluster & Task Definitions

Go to ECS > Clusters > Create Cluster

Launch Fargate (serverless) or EC2 type

Create two Task Definitions:

Backend container (Port 5000)

Frontend container (Port 3000)

Use ECR image URLs in container definitions

🌐 4. Configure Networking (VPC)

Create VPC with 2 public subnets

Configure Security Groups:

Port 5000 (backend)

Port 3000 (frontend)

(Optional) Add Application Load Balancer

✅ 5. Deploy & Verify

Deploy ECS services and verify:

curl http://<BACKEND_PUBLIC_IP>:5000
# {"message": "Hello from Flask backend!"}

curl http://<FRONTEND_PUBLIC_IP>:3000
# Express frontend is running 🚀

📊 Final Project Verification
Component	Status	URL
Backend	✅ Running	http://54.252.159.32:5000

Frontend	✅ Running	http://16.176.232.29:3000
