---
title: Jobfit Checker
date: 2025-05-25
links:
  - name: Source Code
    url: https://github.com/TiansiGu/JobFitCheker-Source
  - name: Infrastructure  
    url: https://github.com/TiansiGu/JobFitChecker-Infra
tags:
  - fullstack web application
  - event-driven architecture
  - CI/CD pipeline
---

Jobfit Checker is a web application that support the users to check if they are qualified to apply for a job based on the job description. It enables the following feature:

- User authentification & session management
- User Resume's upload/update/delete
- Resume postprocessing, which is triggered by AWS SQS and leverages Langchain4J to extract user qualification profile
- User job qualification check
- Track job application history

The [infrastructure repo](https://github.com/TiansiGu/JobFitChecker-Infra/tree/main/.github/workflows) sets up a deployment pipeline that gets triggered by a PR to main branch. The pipeline builds the docker images of the three microservices in the source repo, publish it to ECR, and deploys the new images to a QA EC2 machine. Once QA test is passed, we can trigger the deloyment to UAT environment, which mimcs the prod environment with domains, replicas, and Kubernete clusters. Once UAT is good to go, the blue-green deployment workflow is triggered to finally deploy the newest changes to production.

<!--more-->
