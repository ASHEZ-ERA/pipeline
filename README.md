# Jenkins CI/CD Pipeline with Docker

## Pipeline Stages
Clone → Lint → Test → Build → Push → Deploy

## Tech Stack
- Jenkins (CI/CD orchestration)
- Docker (containerisation)
- Docker Hub (image registry)
- AWS EC2 (hosting)
- Node.js (application)
- Bash (scripting)

## How it works
Every push to main branch automatically triggers Jenkins which 
builds a Docker image, pushes it to Docker Hub, and deploys 
it live on AWS EC2.

## Live Demo
http://your-ec2-ip