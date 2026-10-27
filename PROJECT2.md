Ironhack DevOps Project 2

Deploying a 3-Tier Voting Application on Amazon EKS

Project Overview

In this project, I migrated the Cats vs Dogs voting application from my previous EC2-based infrastructure to Amazon EKS using Kubernetes.

I deployed five microservices, configured external access through NGINX Ingress, and implemented a CI/CD pipeline using GitHub Actions to automate Docker image builds and deployments.

Architecture

The application consists of five components:

Vote: Python application that receives user votes.

Redis: Temporarily stores votes for processing.

Worker: .NET application that processes votes and writes them to PostgreSQL.

PostgreSQL: Stores the processed voting results.

Result: Node.js application that displays voting statistics.

The components communicate through Kubernetes Services, while NGINX Ingress exposes the Vote and Result interfaces.

Technologies Used

Amazon EKS, Kubernetes, Docker, Docker Hub, GitHub Actions, AWS IAM/OIDC, Helm, NGINX Ingress, Python, Node.js, .NET, Redis and PostgreSQL.

CI/CD Implementation

I created a GitHub Actions workflow that automatically:

Builds Docker images for Vote, Result and Worker.

Pushes the images to Docker Hub using commit-based tags.

Authenticates to AWS through an IAM role using OIDC.

Updates the application's Kubernetes Deployments.

Verifies that the new deployments are running successfully.

Validation

I verified that all five Kubernetes Pods were running, both public application interfaces were accessible, and votes were successfully processed and displayed.

I also confirmed that GitHub Actions completed successfully and deployed new container images to EKS.

Challenges and Lessons Learned

One challenge was configuring NGINX Ingress to correctly route the Vote and Result applications. Although both endpoints initially responded, the Result interface displayed a blank page because its JavaScript resources were not loading correctly.

I identified the missing resources using browser Developer Tools and corrected their routing through additional Ingress rules.

This project improved my understanding of container orchestration, Kubernetes networking, AWS authentication and automated application deployment.

Limitations

This is a learning deployment using a single worker node and HTTP endpoints. PostgreSQL currently uses temporary storage rather than a persistent volume. These aspects would require improvement for a production environment.

Repository and CI/CD Evidence

GitHub Repository: https://github.com/AbdulqudusO/example-voting-app

Successful CI/CD Run: https://github.com/AbdulqudusO/example-voting-app/actions/runs/40434847640
