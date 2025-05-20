# Deploying-Application-on-EKS-cluster-using-Github-Actions-CI-CD

## Installed Tools
1. Java JDK 17
2. Maven
3. Docker
4. Git
5. kubectl
6. AWS CLI
7. eksctl (for creating EKS cluster)

## Accounts and Services
1. GitHub Account
2. Docker Hub Account
3. AWS Account
4. SonarQube (Local or Cloud-hosted)

## Step 1: Initialize the Java Project
mkdir Github-Actions-project && cd Github-Actions-project
mvn archetype:generate \
  -DgroupId=com.app \
  -DartifactId=myapp \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -Dintercd activeMode=false
cd myapp
mv * ../ && cd .. && rm -rf myapp

## Step 2: Create Dockerfile

## Step 3: Create Kubernetes Manifests
   deployment.yaml
   service.yaml
   
## Step 4: Configure GitHub Actions Workflow
.github/workflows/main.yml

## Step 5: Configure GitHub Secrets
Add these secrets in GitHub > Settings > Secrets:
DOCKER_USERNAME
DOCKER_PASSWORD
SONAR_TOKEN

## Step 6: Set Up SonarQube Locally
docker pull sonarqube
docker run -d --name sonarqube -p 9000:9000 sonarqube

## Step 7: Create EKS Cluster 
Then run:
eksctl create cluster --name my-cluster --region ap-south-1 --version 1.32 --nodes 2
aws eks update-kubeconfig --name my-cluster --region ap-south-1
kubectl get nodes

## Step 8: Push Code to GitHub

## Step 9: Verify GitHub Actions Execution
Navigate to the Actions tab in your GitHub repo
Observe workflow build, test, image push, and Kubernetes deployment
✅ Maven build succeeded
✅ SonarQube scan uploaded
✅ Docker image pushed to DockerHub
✅ Deployment applied to EKS

## Step 10: Access the App
kubectl get svc
Check EXTERNAL-IP of myapp-service, then open in browser:
http://<EXTERNAL-IP>

Cleanup
eksctl delete cluster --name my-cluster --region ap-south-1
docker stop sonarqube && docker rm sonarqube




