# Ubuntu Jenkins Docker CI/CD

A hands-on DevOps project demonstrating automated web application deployment using Ubuntu Linux, GitHub, Jenkins, Docker, and Nginx.

## Architecture

```text
Developer
   |
   v
GitHub Repository
   |
   v
Jenkins Pipeline
   |
   +--> Checkout
   +--> Validate HTML
   +--> Deploy
   +--> HTTP Smoke Test
   |
   v
Ubuntu Host Directory
   |
   v
Docker Nginx Container
   |
   v
Web Application
```

## Technologies

- Ubuntu Linux
- Java 21
- Jenkins LTS
- Git and GitHub
- Docker Engine
- Docker Compose
- Nginx
- Bash and HTML

## Features

- Source code checkout from GitHub.
- HTML validation using a Jenkins pipeline.
- Automated deployment to an Nginx web server.
- Containerized application hosting.
- HTTP smoke testing after deployment.
- Linux service and deployment troubleshooting.

## Project Structure

```text
ubuntu-jenkins-docker-cicd/
├── index.html
├── Jenkinsfile
├── README.md
└── .gitignore
```

## Installation

Install Java, Jenkins, Git, Docker Engine, and the Docker Compose plugin using their official documentation.

Configure Jenkins to use port 8081 and Nginx to use port 8080 if both run on the same host.

Create the deployment directory:

```bash
sudo install -d -o jenkins -g jenkins -m 0755 /opt/devops-site
```

Configure Nginx with a Docker Compose bind mount from `/opt/devops-site` to `/usr/share/nginx/html`.

## Pipeline Stages

1. **Checkout:** Retrieve source code from GitHub.
2. **Validate:** Check the HTML file and expected content.
3. **Deploy:** Copy the HTML file into the deployment directory.
4. **Smoke Test:** Verify the deployed page through HTTP.

## Verification

```bash
sudo systemctl status jenkins
sudo docker ps
curl -sS http://localhost:8080/
```

A successful deployment should display `Deployment successful!`.

## Troubleshooting

- Jenkins service issues: `sudo journalctl -u jenkins -n 100 --no-pager`
- Container errors: `sudo docker logs devops-nginx`
- Port conflicts: `sudo ss -ltnp`
- Deployment permissions: `ls -ld /opt/devops-site`
- HTTP failures: `curl -v http://localhost:8080/`

## Future Enhancements

- GitHub webhook integration.
- Automated tests and code quality checks.
- Ansible-based configuration management.
- Prometheus and Grafana monitoring.
- Secure remote deployment and HTTPS.

## Author

Jignesh Patel

Linux Administration | DevOps | Cloud Infrastructure | CI/CD

This is a learning and portfolio project. Production use requires additional security, access control, monitoring, and deployment safeguards.
