📘 Node.js Frontend App (Dockerized)

This is a simple Node.js application that serves a static frontend HTML page using Express.
The application is fully containerized using Docker.

🚀 Features

Node.js + Express server

Serves static HTML from public/ folder

Easy to run using Docker

Clean and lightweight setup

📂 Project Structure
.
├── Dockerfile
├── index.js
├── package.json
└── public
    └── index.html

🛠️ Install Dependencies (Local)

If you want to run it locally (not in Docker):

npm install
npm start


App runs at:

👉 http://localhost:3000

🐳 Running with Docker
1. Build Docker image
docker build -t mynodeapp .

2. Run the container
docker run -p 3000:3000 mynodeapp


App will be available at:

👉 http://<your-ec2-ip>:3000
