# Dockerized Python Web Application & CI/CD

A beginner DevOps project demonstrating Python application containerization with Docker and automated CI/CD using GitHub Actions.

## Tech Stack

- Python
- Flask
- Docker
- Git
- GitHub
- GitHub Actions
- Linux

## Project Architecture

Python Application
        ↓
    Dockerfile
        ↓
    Docker Image
        ↓
   Docker Container
        ↓
    Port 5000
        ↓
   Flask Endpoints

## Application Endpoints

### Home

GET /

Returns:

DevOps CI/CD Project is running!

### Health Check

GET /health

Returns:

{"status": "healthy"}

## Run with Docker

Build the image:

docker build -t devops-python-app:1.0 .

Run the container:

docker run -d --name devops-python-container -p 5000:5000 devops-python-app:1.0

## Test the Application

curl http://127.0.0.1:5000

curl http://127.0.0.1:5000/health

## View Container Logs

docker logs devops-python-container

## Docker Concepts Practiced

- Dockerfile
- Docker images
- Docker containers
- Port mapping
- Environment variables
- Container logs
- Docker build and run

## CI/CD

GitHub Actions will be used to automatically build and test the application when changes are pushed to GitHub.

## Project Structure

docker-cicd-python/
├── app.py
├── requirements.txt
├── Dockerfile
├── .dockerignore
├── .gitignore
├── README.md
└── .github/

