# CI/CD Pipeline Project Report

## Project Objective
To build a CI/CD pipeline demonstrating continuous deployment and host the application on an AWS EC2 instance.

## Tools Used
- GitHub for version control
- Jenkins for automation
- AWS EC2 for hosting
- Java for runtime environment
- Spring Boot for the demo application

## Step-by-Step Process

### 1. Setting Up the GitHub Repository
- Created a new repository: https://github.com/kaif2106/CI-CD
- Initialized with a README and .gitignore file for Java projects

### 2. Creating a Spring Boot Demo Application
- Used Spring Initializr to create a basic Spring Boot application
- Added a simple REST controller to return "Hello, World!"
- Pushed the application code to the GitHub repository

### 3. Setting Up AWS EC2 Instance
- Launched a new EC2 instance using Amazon Linux 2023
- Configured security group to allow inbound traffic on ports:
  - 22 (SSH)
  - 80 (HTTP)
  - 8080 (Jenkins)

### 4. Installing and Configuring Java
- Connected to the EC2 instance via SSH
- Installed Java 17:
  ```
  sudo dnf install java-17-amazon-corretto -y
  ```
- Verified Java installation:
  ```
  java -version
  ```

### 5. Installing and Configuring Jenkins
- Added Jenkins repository:
  ```
  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
  ```
- Installed Jenkins:
  ```
  sudo dnf install jenkins -y
  ```
- Started Jenkins service:
  ```
  sudo systemctl start jenkins
  sudo systemctl enable jenkins
  ```
- Retrieved initial admin password:
  ```
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
- Accessed Jenkins via web browser and completed initial setup

### 6. Configuring Jenkins Pipeline
- Installed necessary Jenkins plugins (Git, Pipeline)
- Created a new Pipeline job in Jenkins
- Configured the job to use the GitHub repository

### 7. Creating Jenkinsfile
- Added a Jenkinsfile to the root of the GitHub repository with stages for:
  - Checkout
  - Build
  - Test
  - Deploy

### 8. Configuring GitHub Webhook
- Added a webhook in the GitHub repository settings
- Set the payload URL to the Jenkins server
- Configured it to trigger on push events

### 9. Testing the Pipeline
- Made a change to the application code
- Pushed the change to GitHub
- Verified that the Jenkins pipeline was automatically triggered

### 10. Troubleshooting
- Resolved Java installation issues
- Fixed Jenkins startup problems
- Addressed GitHub connection errors in Jenkins

## Challenges Faced and Solutions

1. **Java Installation**: Initially, Java was not installed on the EC2 instance. This was resolved by installing Amazon Corretto 17.

2. **Jenkins Startup Issues**: Jenkins failed to start initially due to missing Java. This was resolved after proper Java installation.

3. **GitHub Connection**: Jenkins failed to connect to the GitHub repository. This was addressed by:
   - Verifying Git installation on the EC2 instance
   - Checking network connectivity
   - Ensuring correct repository URL in Jenkins configuration

## Conclusion
The CI/CD pipeline was successfully set up, demonstrating continuous deployment of a Spring Boot application to an AWS EC2 instance. The pipeline automatically builds, tests, and deploys the application whenever changes are pushed to the GitHub repository.

## Future Improvements
- Implement more comprehensive testing in the pipeline
- Add staging and production environments
- Implement blue-green deployment strategy
- Enhance security measures (e.g., using IAM roles, implementing HTTPS)

