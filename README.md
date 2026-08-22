Dockerized Python Web Application & CI/CD
A beginner DevOps project demonstrating Python application containerization with Docker, automated testing with GitHub Actions, and Docker image publishing to Docker Hub.
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
```text
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
   +--> Setup Python
   +--> Install Dependencies
   +--> Test Application
   +--> Build Docker Image
   +--> Login to Docker Hub
   +--> Push Docker Image
   |
   v
Docker Hub
```
Application
The project uses a lightweight Python Flask application with two endpoints.
Home Endpoint
Request:
```text
GET /
```
Test:
```bash
curl http://127.0.0.1:5000
```
Example output:
```text
DevOps CI/CD Project V2 is running!
```
Health Endpoint
Request:
```text
GET /health
```
Test:
```bash
curl http://127.0.0.1:5000/health
```
Example output:
```json
{"status":"healthy"}
```
Project Structure
```text
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
```
Run Locally
Create and activate a virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate
```
Install dependencies:
```bash
pip install -r requirements.txt
```
Start the application:
```bash
python app.py
```
Expected output:
```text
* Serving Flask app 'app'
* Debug mode: off
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:5000
```
Docker
Build the Image
```bash
docker build -t devops-python-app:1.0 .
```
Expected result:
```text
[+] Building ... FINISHED
=> naming to docker.io/library/devops-python-app:1.0
```
Run the Container
```bash
docker run -d --name devops-python-container -p 5000:5000 devops-python-app:1.0
```
Check the container:
```bash
docker ps
```
Example:
```text
CONTAINER ID   IMAGE                  STATUS       PORTS
xxxxxxxxxxxx   devops-python-app:1.0 Up ...       0.0.0.0:5000->5000/tcp
```
Test the Container
```bash
curl http://127.0.0.1:5000
```
Output:
```text
DevOps CI/CD Project V2 is running!
```
```bash
curl http://127.0.0.1:5000/health
```
Output:
```json
{"status":"healthy"}
```
View Container Logs
```bash
docker logs devops-python-container
```
Example:
```text
* Serving Flask app 'app'
* Debug mode: off
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:5000
172.17.0.1 - - "GET / HTTP/1.1" 200 -
172.17.0.1 - - "GET /health HTTP/1.1" 200 -
```
HTTP status `200` indicates successful requests.
GitHub Actions
The workflow is located at:
```text
.github/workflows/ci.yml
```
The workflow runs automatically when code is pushed to `main` and when a pull request targets `main`.
Pipeline
```text
git push
   |
   v
GitHub Actions
   |
   +--> Checkout repository
   +--> Setup Python 3.12
   +--> Install dependencies
   +--> Validate Python application
   +--> Start Flask application
   +--> Test / endpoint
   +--> Test /health endpoint
   +--> Build Docker image
   +--> Login to Docker Hub
   +--> Push Docker image
   |
   v
Success
```
Automated Application Tests
The pipeline validates Python syntax:
```bash
python -m py_compile app.py
```
It then starts the Flask application and checks both endpoints:
```bash
curl --fail http://127.0.0.1:5000/
curl --fail http://127.0.0.1:5000/health
```
Successful pipeline stages:
```text
Checkout repository       ✓
Set up Python             ✓
Install dependencies      ✓
Test application          ✓
Build Docker image        ✓
Log in to Docker Hub      ✓
Push Docker image         ✓
```
Docker Hub
The Docker image is published automatically to:
```text
re1r0/docker-cicd-python
```
Image:
```text
re1r0/docker-cicd-python:latest
```
Pull the published image:
```bash
docker pull re1r0/docker-cicd-python:latest
```
Example:
```text
latest: Pulling from re1r0/docker-cicd-python
Status: Downloaded newer image for re1r0/docker-cicd-python:latest
docker.io/re1r0/docker-cicd-python:latest
```
Run the Published Image
```bash
docker run -d   --name dockerhub-test   -p 5001:5000   re1r0/docker-cicd-python:latest
```
Check:
```bash
docker ps
```
Test:
```bash
curl http://127.0.0.1:5001
```
Output:
```text
DevOps CI/CD Project V2 is running!
```
Health check:
```bash
curl http://127.0.0.1:5001/health
```
Output:
```json
{"status":"healthy"}
```
CI Failure Testing
The pipeline was intentionally tested with a Python syntax error.
Broken code:
```python
return {"status": "healthy"
```
GitHub Actions detected the error during:
```bash
python -m py_compile app.py
```
Example failure:
```text
SyntaxError: '{' was never closed
Process completed with exit code 1
```
Because the application test failed, the Docker build did not continue.
The code was corrected to:
```python
return {"status": "healthy"}
```
After pushing the fix, the GitHub Actions pipeline completed successfully.
DevOps Concepts Practiced
Git version control
GitHub repositories
Git commits and branches
Dockerfiles
Docker images
Docker containers
Port mapping
Container logs
Application health checks
GitHub Actions
Continuous Integration
Automated application testing
Docker image building
Docker Hub
Container image publishing
CI failure troubleshooting
Project Outcome
The project demonstrates an automated workflow from source code to a published Docker image:
```text
Developer
   |
   | git push
   v
GitHub
   |
   v
GitHub Actions
   |
   +--> Test application
   +--> Build Docker image
   +--> Publish image
   |
   v
Docker Hub
```
The published Docker image was independently pulled from Docker Hub and successfully executed as a Docker container.
Current Scope
This project currently demonstrates CI and automated Docker image delivery.
Automated server deployment has not yet been implemented.
Future Improvements
Automated deployment to a server
AWS EC2 deployment
Docker image versioning
Production WSGI server
Automated rollback
Monitoring and logging
