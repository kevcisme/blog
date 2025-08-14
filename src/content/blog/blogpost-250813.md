---
title: Back in the Saddle with Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-08-13 9:20
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

In June, we merged a small but important UX fix to stabilize the navigation dropdowns. Since then, we focused on hardening our infrastructure, clarifying deployment, and polishing a few aspects of the app. This post summarizes the most meaningful changes from my last post.
### Highlights

- **Infrastructure as Code (Terraform)**
  - Finalized a full Terraform setup under `terraform/` to provision the app's AWS foundation: VPC, subnets, security groups, IAM, RDS, S3, ECR, ACM, and an EC2 module with `user_data` bootstrap.
  - Added environment-specific variables for `dev` and `prod`, plus consolidated variables and outputs. Deployment docs included.
- **Deployment and Ops**
  - Updated Docker assets and `docker-compose.prod.yml`; added `backend/Dockerfile.prod` and an `nginx/nginx.conf` for production reverse proxying.
  - Added `scripts/setup-aws-infrastructure.sh` and deployment examples (`deploy-example.yml`, `main-example.yml`).
  
- **Frontend and middleware**
  - Minor refinements to `src/components/Navigation.tsx` and the community Q&A page at `src/app/community/[questionId]/page.tsx`.
  - Introduced `src/middleware.ts` to support runtime behaviors at the edge (e.g., redirects/headers), paving the way for future platform features.
- **Developer experience**
  - Added a `Makefile` for common tasks and several example env/config files (`.env.local.backup`, `env.prod.example`).
  - Dependency housekeeping in `package.json` and `package-lock.json`.

### By the numbers

- I've changed **54 files**, **6181 insertions**, **557 deletions**

### What this enables

- **Repeatable infrastructure**: Teams can stand up and evolve environments with code review and versioning.
- **Clearer deployments**: Docker, Nginx, and example pipeline files make the release path easier to follow and automate.
- **Operational guardrails**: Middleware and config defaults reduce drift and support future auth/routing behaviors.

### Getting started (at a glance)

- Review the infrastructure docs in `terraform/TERRAFORM_DEPLOYMENT.md` and `AWS_DEPLOYMENT.md`.
- Use the `Makefile` targets and example YAML files to scaffold CI/CD, and `nginx/nginx.conf` for production reverse proxy.
- Sync local/env variables from the provided examples (`env.prod.example`, `.env.local.backup`).
