# CI-CD-Pipeline-with-AWS
CI/CD Pipeline with AWS CodePipeline for EC2 Deployment
This project sets up a CI/CD pipeline on AWS that automates the process of building, testing, and deploying an application to an EC2 instance. Below is a breakdown of how each AWS service plays its role.

Goal

To automate the building, testing, and deployment of an application hosted on an AWS EC2 instance using AWS CodePipeline.

Workflow Overview
	1.	Developer Pushes Code → CodeCommit Repository
	2.	CodePipeline Triggers Build → CodeBuild compiles the code
	3.	CodePipeline Triggers Testing → Lambda executes automated tests
	4.	CodePipeline Triggers Deployment → CodeDeploy deploys the latest build to EC2

 🔹 AWS Services Used & Their Roles

1️⃣ AWS CodeCommit (Source Control)
	•	Purpose: Stores the application’s source code in a Git repository.
	•	How It Works: Developers push code to the repository, which triggers the pipeline.

2️⃣ AWS CodePipeline (CI/CD Orchestration)
	•	Purpose: Automates the workflow for fetching, building, testing, and deploying the application.
	•	How It Works:
	•	Triggers whenever there’s a new commit in CodeCommit.
	•	Calls CodeBuild to build the project.
	•	Calls Lambda to run tests.
	•	Calls CodeDeploy to deploy the app to EC2.

3️⃣ AWS CodeBuild (Build Stage)
	•	Purpose: Compiles the code, runs unit tests, and prepares artifacts for deployment.
	•	How It Works:
	•	Uses a buildspec.yml file to define the build process.
	•	Generates an artifact (e.g., a .zip file) and stores it in S3 for deployment.

4️⃣ AWS Lambda (Test Stage)
	•	Purpose: Runs automated tests after the build is complete.
	•	How It Works:
	•	Lambda is triggered in the pipeline to execute test cases.
	•	If the test fails, the pipeline stops.

5️⃣ AWS CodeDeploy (Deployment Stage)
	•	Purpose: Deploys the built application to an EC2 instance.
	•	How It Works:
	•	Uses an AppSpec.yml file to define how the deployment is done.
	•	Handles stopping the old application and starting the new version on EC2.

6️⃣ Amazon EC2 (Compute for Application)
	•	Purpose: Hosts the web application.
	•	How It Works:
	•	Receives the deployed build via CodeDeploy.
	•	Runs the application using Apache/Nginx or any application server.

7️⃣ Amazon S3 (Artifact Storage)
	•	Purpose: Stores the build artifacts before deployment.
	•	How It Works:
	•	CodeBuild uploads built artifacts (e.g., .zip files) to an S3 bucket.
	•	CodeDeploy retrieves them from S3 to deploy on EC2.

8️⃣ AWS IAM (Security & Permissions)
	•	Purpose: Controls access between services.
	•	How It Works:
	•	IAM Roles for CodeBuild, CodeDeploy, and EC2 to interact securely.
	•	IAM Policies define permissions (e.g., allowing EC2 to access S3).

 📌 CI/CD Pipeline Execution Flow
	1.	Code Commit:
	•	Developer pushes code to AWS CodeCommit.
	•	CodePipeline detects the change.
	2.	Build Stage (AWS CodeBuild):
	•	CodeBuild runs based on buildspec.yml.
	•	Builds the code and packages it into a deployable artifact.
	•	Uploads the artifact to Amazon S3.
	3.	Testing Stage (AWS Lambda):
	•	Lambda runs automated test cases.
	•	If tests fail, the pipeline stops.
	4.	Deployment Stage (AWS CodeDeploy):
	•	Fetches the artifact from Amazon S3.
	•	Deploys the application to EC2 using AppSpec.yml.
	•	Ensures zero-downtime deployment (if needed).
	5.	Application is Live on EC2! 🚀
	•	Users can access the newly deployed app.

 🔥 Key Benefits of This CI/CD Pipeline

✅ Automation – No manual intervention needed for deployments.
✅ Faster Releases – Code is built, tested, and deployed in minutes.
✅ Consistency – Same process runs every time, reducing errors.
✅ Scalability – Can extend to multiple EC2 instances or ECS in the future.
