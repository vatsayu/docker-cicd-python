Dockerized Python Web Application & CI/CD

A beginner DevOps project demonstrating Python application containerization with Docker and automated CI/CD using GitHub Actions and Docker Hub.

Tech Stack

Python

Flask

Docker

Git

GitHub

GitHub Actions

Docker Hub

Linux

Project Architecture

Developer
|
| git push
v
GitHub Repository
|
v
GitHub Actions
|
+--> Checkout Repository
+--> Setup Python 3.12
+--> Install Dependencies
+--> Test Application
+--> Build Docker Image
+--> Login to Docker Hub
+--> Push Docker Image
|
v
Docker Hub

Application

The project uses a lightweight Python Flask application with two endpoints.

Home Endpoint

Request:

GET /

Command:

curl http://127.0.0.1:5000

Output:

DevOps CI/CD Project V2 is running!

Health Endpoint

Request:

GET /health

Command:

curl http://127.0.0.1:5000/health

Output:

{"status":"healthy"}

Project Structure

docker-cicd-python/
├── app.py
├── requirements.txt
├── Dockerfile
├── .dockerignore
├── .gitignore
├── README.md
└── .github/
    └── workflows/
        └── ci.yml

Run Application Locally

python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py

Expected output:

* Serving Flask app 'app'
* Debug mode: off
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:5000

Docker Build

docker build -t devops-python-app:1.0 .

Expected result:

[+] Building ... FINISHED
=> naming to docker.io/library/devops-python-app:1.0

Run Docker Container

docker run -d --name devops-python-container -p 5000:5000 devops-python-app:1.0

Check:

docker ps

Example:

CONTAINER ID   IMAGE                  STATUS       PORTS
xxxxxxxxxxxx   devops-python-app:1.0 Up ...       0.0.0.0:5000->5000/tcp

Test Docker Container

curl http://127.0.0.1:5000

Output:

DevOps CI/CD Project V2 is running!

curl http://127.0.0.1:5000/health

Output:

{"status":"healthy"}

Container Logs

docker logs devops-python-container

Example:

* Serving Flask app 'app'
* Debug mode: off
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:5000
172.17.0.1 - - "GET / HTTP/1.1" 200 -
172.17.0.1 - - "GET /health HTTP/1.1" 200 -

HTTP status 200 indicates successful requests.

GitHub Actions CI/CD

Workflow:

.github/workflows/ci.yml

The workflow runs automatically when code is pushed to the main branch or when a pull request targets main.

Pipeline

Git Push
   |
   v
GitHub Actions
   |
   +--> Checkout Repository
   +--> Setup Python 3.12
   +--> Install Dependencies
   +--> Validate Python Application
   +--> Start Flask Application
   +--> Test Application Endpoints
   +--> Build Docker Image
   +--> Login to Docker Hub
   +--> Push Docker Image
   |
   v
SUCCESS

Application Testing

python -m py_compile app.py
curl --fail http://127.0.0.1:5000/
curl --fail http://127.0.0.1:5000/health

Successful stages:

Checkout repository       ✓
Set up Python             ✓
Install dependencies      ✓
Test application          ✓
Build Docker image        ✓
Log in to Docker Hub      ✓
Push Docker image         ✓

Docker Hub

Repository:

re1r0/docker-cicd-python

Image:

re1r0/docker-cicd-python:latest

Pull:

docker pull re1r0/docker-cicd-python:latest

Example:

latest: Pulling from re1r0/docker-cicd-python
Status: Downloaded newer image for re1r0/docker-cicd-python:latest
docker.io/re1r0/docker-cicd-python:latest

Run Docker Hub Image

docker run -d --name dockerhub-test -p 5001:5000 re1r0/docker-cicd-python:latest

Check:

docker ps

Test:

curl http://127.0.0.1:5001

Output:

DevOps CI/CD Project V2 is running!

Health check:

curl http://127.0.0.1:5001/health

Output:

{"status":"healthy"}

CI Failure Testing

The CI pipeline was intentionally tested with a Python syntax error.

Broken code:

return {"status": "healthy"

GitHub Actions detected the error during:

python -m py_compile app.py

Example failure:

SyntaxError: '{' was never closed
Process completed with exit code 1

The Docker build did not continue because the application test failed.

The code was corrected:

return {"status": "healthy"}

After pushing the fix, GitHub Actions successfully completed the pipeline.

DevOps Concepts Practiced

Git version control

GitHub repositories

Git commits and branches

Dockerfiles

Docker images

Docker containers

Port mapping

Container logs

Health checks

GitHub Actions

Continuous Integration

Automated application testing

Docker image building

Docker Hub

Container image publishing

CI failure troubleshooting

Project Outcome

Developer
    |
    | git push
    v
GitHub
    |
    v
GitHub Actions
    |
    +--> Test Application
    +--> Build Docker Image
    +--> Publish Image
    |
    v
Docker Hub

The published Docker image was independently pulled from Docker Hub and successfully executed as a container.

Future Improvements

Automated deployment to a server

AWS EC2 deployment

Docker image versioning

Production WSGI server

Automated rollback

Monitoring and logging