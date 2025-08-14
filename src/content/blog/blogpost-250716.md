---
title: Terraform with Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-07-16 9:20
author: Kevin Coyle
tags:
  - Adventure
  - Full Stack Development
  - IaC
  - Terraform
imgUrl: '../../assets/dude-scouts.png'
layout: ../../layouts/BlogPost.astro
---

# Devops let's goooo

## From Events to Enterprise: What changed between “meeting page” and now

Here’s a concise tour of the work that transformed the project from a polished meetings page into a production-ready, cloud-deployable platform with infra-as-code, reverse proxying, and a cleaner developer workflow.

I had the pleasure to work in this cool pattern with a friend/CTO Nash Taylor. He wrote this whole set up where PRs would spin up an environment where we could play with the app. I wrote a bunch of Terraform stuff to start to try to replicate this process. Also, I wanted to get back into the swing of writing Terraform stuff.

### TL;DR

- Infrastructure-as-code added with Terraform (VPC, EC2, ECR, RDS, S3, DynamoDB, ACM, IAM, Security Groups).
- Production Docker setup hardened (compose, Nginx reverse proxy, prod Dockerfiles).
- One-command developer ergonomics with a new Makefile.
- Deployment docs and AWS setup scripts added.
- Frontend expanded (Dude Chat page), enhanced navigation, and middleware added.

### Infrastructure & DevOps

- Terraform introduced under `terraform/` with modular design:
  - Modules for `vpc`, `ec2`, `ecr`, `rds`, `s3`, `dynamodb`, `acm`, `iam`, `security-groups`
  - Environment overlays: `terraform/environments/dev/terraform.tfvars` and `.../prod/...`
  - Root wiring and outputs (`main.tf`, `variables.tf`, `outputs.tf`, `versions.tf`)
  - Deployment notes: `terraform/TERRAFORM_DEPLOYMENT.md`
- Nginx reverse proxy added for production
  - Config in `nginx/nginx.conf` to front Next.js and FastAPI behind 80/443
- Docker and Compose hardened
  - `docker-compose.prod.yml` updated for prod services and health checks
  - Backend prod image split: `backend/Dockerfile.prod`
  - Repo-level `Dockerfile` and `.dockerignore` updated for smaller builds
- One-command local and CI helpers
  - `Makefile` with targets for dev/test/lint/format/logs/clean
  - `scripts/setup-aws-infrastructure.sh` to bootstrap AWS resources
  - Env scaffolding: `.env.local.backup`, `env.prod.example`, `main-example.yml`, `deploy-example.yml`
- Documentation
  - `AWS_DEPLOYMENT.md` and `GITHUB_CONFIGURATION.md` added for CI/CD and platform setup
  - Screenshot references and prod compose docs updated

### App & Frontend

- Meetings page (previously shipped) was the stepping stone. Since then:
  - New page: `src/app/community/dude-chat/page.tsx` (community engagement surface)
  - Navigation enhancements in `src/components/Navigation.tsx` to expose new sections
  - Middleware added (`src/middleware.ts`) to prep for auth/routing concerns
  - Community detail page edits: `src/app/community/[questionId]/page.tsx` UI polish

### Why this matters

- Repeatable infra: Terraform lets you bring up/down consistent dev/prod stacks.
- Secure, scalable edge: Nginx centralizes TLS and routing, simplifying service topology.
- Faster iteration: Makefile + scripts reduce yak-shaving for common tasks.
- CI/CD readiness: Clear docs + examples accelerate pipeline setup and secrets configuration.
- Product surface growth: Community chat and nav improvements increase engagement and discovery.

### What to do next

- Wire Terraform outputs into GitHub Actions variables to fully automate deploys.
- Add health and smoke checks post-deploy (curl API, ping frontend).
- Route logs/metrics to CloudWatch or another aggregator.
- Expand middleware to enforce auth where needed (e.g., chat).
- Gradually swap mock data for real services (DB, queues, analytics events).

- New infra-as-code (`terraform/`) and prod Nginx/Compose assets added.
- Makefile and scripts streamline local dev and deployment.
- Community features expanded (Dude Chat), navigation and middleware added.
- Docs and env scaffolding round out a CI/CD-ready, production-focused repo.