Overview
This project uses CircleCI to automate the build and deployment processes. The configuration file .circleci/config.yml defines the steps and workflows for building and deploying the project.


Jobs
1. Build Job

Description: Building the project.
Machine: Ubuntu 20.04
Docker Layer Caching: Enabled
Steps:

checkout: Fetch the source code.
Installing AWS CLI: Install AWS CLI for deployment.
npm install && npm run build: Install dependencies and build the project.
persist_to_workspace: Save the build artifacts to the workspace.

2. Deploy Job

Description: Deploying the code to AWS S3 Bucket.
Machine: Ubuntu 20.04
Docker Layer Caching: Enabled
Steps:

attach_workspace: Attach the workspace from the build job.
checkout: Fetch the source code.
Configuring AWS: Configure AWS credentials.
aws s3 sync: Sync the build artifacts with the specified S3 bucket (only on the master branch).
Workflows
Execute Bulk Workflow
Jobs:

build: Build the project.
deploy: Deploy the project to AWS S3 Bucket.
Conditions:

The deploy job requires the successful completion of the build job.
The deploy job is triggered only on the master branch.
Getting Started
Clone the Repository:

bash
Copy code
git clone <repository-url>
cd <repository-directory>
Configure AWS Credentials:

Ensure AWS CLI is installed.
Configure AWS credentials with necessary permissions.
Run Locally:

Build the project locally using:
bash
Copy code
cd app
npm install
npm run build
Deploy to AWS S3 manually if needed.
Notes
The project uses CircleCI for continuous integration and deployment.
The AWS S3 deployment is configured to trigger only on the master branch.

