# Deploy Docker container on AWS ECS using AWS ECR

This repository demonstrates how to deploy your own Docker container to AWS ECS by using AWS ECR as container registry.
You can use Docker hub as your resistry also.
<!--- this is a comment--->

## Prerequisite

-[Install Docker](https://docs.docker.com/install/)

-[Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

## Step 1: Push your docker image to AWS ECR

1. Create a repository on AWS ECR

```bash
aws ecr create-repository --repository-name docker-demo
```

2. Login to AWS ECR

```bash
aws ecr get-login --no-include-email --region us-east-1
```

Or fully authenticate:

```bash
aws ecr get-login --no-include-email --region us-east-1 | sh
```

3. Tag your image with the AWS ECR registry

```bash
docker tag dockerdemo aws_account_id.dkr.ecr.region.amazonaws.com/docker-demo
```

4. Push your image to AWS ECR

```bash
docker push aws_account_id.dkr.ecr.region.amazonaws.com/docker-demo
```

## Step 2: Create a ECS Cluster

1. Choose Networking only template

2. Name your cluster and choose default VPC or create a new VPC

## Step 3: Create a Task Definition

1. Name your Task Definition

2. Choose Fargate (you can think fargate as serverless, you don't need to provision your service)

3. Choose "ecsTaskExecutionRole" for Task Role

## Step 4: Add Container to Task Definition

1. Name your container

2. Link your Image URI

3. Port mapping set to your docker port (8080 for me)

## Step 5: Run Task under Cluster

1. Click Run New Task under Tasks tab in Cluster

2. Submit the details by clicking on Run

3. Click on the task, you will get the public Ip for your running service

4. Go to your publicIp:8080 to see you running services.
