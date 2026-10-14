
Jenkins + Docker CI/CD Pipeline
================================

1. Project Overview
-------------------

This project demonstrates a CI/CD workflow using Jenkins, Docker, GitHub, Python Flask, and automated testing. The application exposes REST endpoints and runs inside a Docker container using Gunicorn.

The objective is to automate the process of retrieving source code, running tests, building a Docker image, deploying the application, and verifying its health through a Jenkins pipeline.

2. Project Objectives
--------------------

- Integrate GitHub with Jenkins for source code management.
- Automate application testing using pytest.
- Build a Docker image for the Flask application.
- Run the application inside a Docker container.
- Verify application health through HTTP endpoints and container logs.
- Automate build, test, and deployment stages using Jenkins.

3. Technology Stack
-------------------

- CI/CD: Jenkins
- Containerisation: Docker
- Application: Python and Flask
- Application Server: Gunicorn
- Automated Testing: pytest
- Version Control: Git and GitHub
- Environment: Linux / WSL

4. Project Structure
--------------------

```text
jenkins-docker-cicd/
├── app/
│   ├── app.py
│   └── requirements.txt
├── tests/
│   └── test_app.py
├── Dockerfile
├── .gitignore
└── README.md
```

5. Application Endpoints
------------------------

| Endpoint | Description |
|---|---|
| `/` | Returns application information and running status |
| `/health` | Returns the application health status |

The health endpoint returns HTTP status code 200 when the application is healthy.

6. Prerequisites
----------------

Install the following tools before running the project:

- Python 3
- pip
- Git
- Docker
- Jenkins (required for pipeline automation)

7. Local Setup and Testing
--------------------------

Step 1: Clone the Repository

```bash
git clone https://github.com/dhairyashilrasal-code/jenkins-docker-cicd.git
cd jenkins-docker-cicd
```

Step 2: Create a Virtual Environment

```bash
python3 -m venv .venv
```

Step 3: Activate the Virtual Environment

```bash
source .venv/bin/activate
```

Step 4: Install Dependencies

```bash
pip install -r app/requirements.txt
```

Step 5: Run Automated Tests

```bash
pytest -v
```

Verified result: 2 tests passed.

The tests verify the home endpoint response and the application health endpoint.

8. Docker Build and Execution
-----------------------------

Step 1: Build the Docker Image

Run this command from the project root:

```bash
docker build -t jenkins-docker-cicd:v2 .
```

Step 2: Start the Application Container

```bash
docker run -d --name jenkins-cicd-app -p 5001:5000 jenkins-docker-cicd:v2
```

Port mapping:

- Host port: 5001
- Container port: 5000

Step 3: Verify the Application

Check the home endpoint:

```bash
curl http://localhost:5001/
```

Check the health endpoint:

```bash
curl http://localhost:5001/health
```

Expected health response:

```json
{"status":"healthy"}
```

Step 4: Inspect Container Logs

```bash
docker logs --tail 20 jenkins-cicd-app
```

The container uses Gunicorn as its application server.

9. Planned Jenkins CI/CD Workflow
---------------------------------

The intended Jenkins pipeline will contain the following stages:

1. Checkout: Retrieve the latest source code from GitHub.
2. Test: Install the required dependencies and execute pytest.
3. Build: Build the Docker image after successful tests.
4. Deploy: Start or update the application container.
5. Verify: Check the health endpoint and inspect deployment logs.

The pipeline should stop if automated tests fail, preventing an unsuccessful build from proceeding to deployment.

Implementation status: The Flask application, automated tests, Docker image, container execution, and GitHub source tracking have been completed and verified. Jenkins integration and automated deployment remain pending verification.

10. Version Control
-------------------

The project is maintained in Git and hosted on GitHub.

Repository: https://github.com/dhairyashilrasal-code/jenkins-docker-cicd

The .gitignore file excludes local virtual environments, Python cache files, test cache files, environment files, and editor-specific files.

11. Future Improvements
-----------------------

- Configure Jenkins to retrieve source code from GitHub.
- Automate testing and Docker image builds.
- Automate container deployment and health verification.
- Trigger pipeline execution after a new GitHub push.
- Add final pipeline documentation and end-to-end verification.



