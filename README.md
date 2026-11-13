# QuakeWatch - DevOps Course Project

Final project of the DevOps Experts course: taking a Flask application from a container on a laptop to Kubernetes on AWS, phase by phase.

> **Credit:** The Flask application in [`app/`](app/) was provided by the course
> ([original repo](https://github.com/EduardUsatchev/QuakeWatch)).
> **My work:** everything in the `phase*` folders and the documentation.

## The application
QuakeWatch is a Flask web dashboard that shows real-time and historical earthquake data from the USGS API. Details: [app/README.md](app/README.md)

## Project phases
| Phase | Topic | Status |
|---|---|---|
| 1 | [Foundation - Docker](phase1-docker/) | ✅ Done |
| 2 | [Orchestration - Kubernetes Basics & Advanced](phase2-kubernetes/) | Coming soon |
| 3 | [Automation - Package Management, Version Control & CI/CD](phase3-helm-cicd/) | Coming soon |
| 4 | [Terraform & AWS](phase4-terraform-aws/) | Coming soon |

### Phase 1: Foundation - Docker
Containerize the application: Dockerfile, Docker Compose, and an image published to Docker Hub.

### Phase 2: Orchestration – Kubernetes Basics & Advanced
Deploy to Kubernetes (Docker Desktop): Deployment, Service, ConfigMaps, Secrets, HPA,
a CronJob that checks the app is up, and liveness/readiness probes.

### Phase 3: Automation – Package Management, Version Control & CI/CD
Helm chart, GitHub Actions (pylint and image build on feature branches, push to Docker Hub
on merge to main), and GitOps with ArgoCD.

### Phase 4: Terraform & AWS
Provision a VPC, security group and EC2 instance with Terraform, install K3s with user data,
and deploy the Helm chart.

## Quick start
```bash
docker pull yelenazamansky/quakewatch:1.0
docker run --rm -p 5000:5000 yelenazamansky/quakewatch:1.0
```
Open http://localhost:5000