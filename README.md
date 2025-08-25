# End-to-End Multi-Cloud CI/CD Pipeline for a .NET Application

This project demonstrates the design and implementation of two complete, automated CI/CD pipelines for an ASP.NET Core web application, deployed to Amazon Web Services (AWS). It serves as a practical, hands-on example of applying core DevOps principles in a multi-cloud environment.

## Live Deployments

*   **AWS Deployment:** [http://helloworldapp-env.eba-ikkmtqvv.ap-south-1.elasticbeanstalk.com/]

---

## Project Overview

The primary objective of this project was to automate the entire software delivery lifecycle, from a `git push` in a source code repository to a live, publicly accessible web application. By building parallel pipelines on both Azure and AWS, this project showcases proficiency in the native DevOps toolchains of the two leading cloud providers.

### Core Concepts Demonstrated:
*   **Continuous Integration (CI):** Code is automatically built and tested upon every commit.
*   **Continuous Deployment (CD):** Successful builds are automatically deployed to the hosting environment.
*   **Infrastructure as Code (IaC):** The build process for AWS is defined in a `buildspec.yml` file, ensuring it is version-controlled and repeatable.
*   **Cloud Security:** Secure connections are established using identity and access management best practices (IAM Roles in AWS).


---

## Architecture Diagrams

### 1. AWS CodePipeline Architecture


**Workflow:**
1.  Developer pushes code to a **GitHub** repository.
2.  **AWS CodePipeline** detects the change and starts the execution.
3.  **Build Stage:** The pipeline invokes **AWS CodeBuild**, which:
    *   Pulls the source code from GitHub.
    *   Reads `buildspec.yml` to execute build commands (.NET 8 SDK).
    *   Produces a zipped, deployable artifact and stores it in S3.
4.  **Deploy Stage:** The pipeline invokes **AWS CodeDeploy** (managed by the pipeline), which:
    *   Takes the artifact from the build stage.
    *   Deploys the new application version to the **AWS Elastic Beanstalk** environment.

---

## Technologies Used

| Category            | AWS Implementation                                       
|---------------------|----------------------------------------------------------|
| **Cloud Platform**  | Amazon Web Services (AWS)                                |
| **CI/CD Service**   | AWS Developer Tools (CodePipeline, CodeBuild)            |
| **Source Control**  | GitHub (Git)                                             |
| **Compute/Hosting** | AWS Elastic Beanstalk                                    |
| **Security/IAM**    | AWS Identity and Access Management (IAM Roles & Policies)|
| **Build Definition**| YAML (`buildspec.yml`)                                   |
| **Framework**       | ASP.NET Core (.NET 8)                                    |

---

## Challenges & Troubleshooting

A key part of this project involved practical, real-world troubleshooting. I successfully diagnosed and resolved:
*   **AWS:**
    *   A policy change by AWS preventing the use of CodeCommit for new users, requiring a pivot to a GitHub-integrated architecture.
    *   Persistent IAM permission propagation delays in the AWS console, which required using the AWS CLI and JSON editing to bypass UI caching issues and correctly configure the pipeline.
    *   .NET SDK version mismatches between the project and the default CodeBuild environment, resolved by explicitly defining the runtime version in `buildspec.yml`.

This hands-on problem-solving was critical to understanding the nuances of cloud security and operations.
