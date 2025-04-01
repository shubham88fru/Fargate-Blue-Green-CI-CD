# Fargate-Blue-Green-CI-CD

---

- Execute these commands from AWS Cloudshell.

## STEP 1: BUILD/TAG/PUSH Image to ECR

1. aws ecr create-repository --repository-name nginx --region us-east-1

<!---
assuming that you have nginx(or any other image of choice on the box)
-->

2. docker tag nginx:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

3. aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

4. docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

---

---

## STEP 2: ECS Task and Setup LB

1. aws ecs register-task-definition --cli-input-json file://taskdef.json

2. Create an ALB with two listeners (at :80 and :8080) and pointing to two target groups. Make sure you attach a security group that allows traffic on :80 and :8080

---

---

## STEP 3: ECS Cluster and Service

1. Create a ESC Fargate cluster from console.

2. aws ecs create-service --service-name my-service --cli-input-json file://create-service.json

---
