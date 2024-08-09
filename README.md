
# MyApp CI/CD Pipeline

This repository contains a CI/CD pipeline for deploying a simple web application to AWS ECS using GitHub Actions. The pipeline includes steps for building, pushing Docker images, and deploying to ECS, with rollback functionality in case of failures.

## Setting Up AWS Resources

1. **Create an ECR Repository**:
   - Navigate to the Amazon ECR console.
   - Click `Create repository` and follow the prompts to create a new repository. Name it `myapp-ecr-repo`.

2. **Create an ECS Cluster**:
   - Navigate to the Amazon ECS console.
   - Click `Create cluster`, choose `EC2 Linux + Networking`, and follow the setup instructions. Name it `myapp-prod-ecs-cluster`.

3. **Create a Task Definition**:
   - Go to the Amazon ECS console.
   - Click `Task Definitions`, then `Create new Task Definition`.
   - Choose `FARGATE` and configure the task definition as needed. Use the `ecs-task-def.json` file in the repository.

4. **Create an IAM Role for ECS**:
   - Go to the IAM console.
   - Create a new role with the `AmazonECSTaskExecutionRolePolicy` policy. Name it `ecsTaskExecutionRole`.

5. **Create a VPC, Subnets, and Security Groups** 
   - Follow AWS documentation to set up a VPC, subnets, and security groups suitable for ECS.

## Configuring GitHub Secrets

1. **Navigate to Secrets**:
   - Go to your GitHub repository.
   - Click on `Settings` > `Secrets and variables` > `Actions`.

2. **Add Secrets**:
   - Click `New repository secret` for each of the following:
     - `AWS_ACCESS_KEY_ID`: Your AWS Access Key ID.
     - `AWS_SECRET_ACCESS_KEY`: Your AWS Secret Access Key.
     - `AWS_REGION`: The AWS region where your ECR repository and ECS cluster are located .
     - `ECR_REPOSITORY`: The name of your ECR repository  `myapp-ecr-repo`.
     - `ECS_CLUSTER`: The name of your ECS cluster  `myapp-prod-ecs-cluster`.
     - `ECS_SERVICE`: The name of your ECS service  `myapp-service`.
     - `TASK_DEFINITION`: The name of your ECS task definition  `myapp-task-def`.

## Testing the Pipeline

1. **Push Changes to GitHub**:
   - Make sure your changes are committed and pushed to the `main` branch:
     ```bash
     git add .
     git commit -m "Add CI/CD pipeline"
     git push origin main
     ```

2. **Monitor GitHub Actions**:
   - Go to the `Actions` tab of your repository on GitHub.
   - Monitor the workflow runs to ensure it completes successfully.

3. **Verify Deployment**:
   - Check the ECS console to verify that the deployment is successful.
   - Review the logs and ensure that the application is running correctly.
