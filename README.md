# Fargate-Blue-Green-CI-CD

---

## STEP 1: BUILD/TAG/PUSH Image to ECR

1. aws ecr create-repository --repository-name nginx --region us-east-1

<!---
assuming that you have nginx(or any other image of choice on the box)
-->

2. docker tag nginx:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

3. aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

4. docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/nginx:latest

---

## STEP 2:
