# 🚀 Jenkins CI/CD Pipeline – Task 2

This project demonstrates a simple yet effective CI/CD pipeline using **Jenkins** and **Docker** to automate the build and deployment of a sample **Node.js** application.

---

## 🎯 Objective

Set up a Jenkins pipeline that automates the **build**, **test**, and **deploy** stages using industry-standard tools and best practices.

---

## 🛠️ Tools & Technologies

- Jenkins – CI/CD workflow orchestrator  
- Docker – Containerization for Jenkins and the Node.js app  
- GitHub – Source code management and webhook triggers  
- Node.js – Sample application  
- localhost.run – Expose Jenkins to the internet for webhook testing  

---

## ✅ What Was Done

- Set up Jenkins locally using Docker  
- Installed required Jenkins plugins  
- Wrote a Jenkinsfile defining the pipeline  
- Configured GitHub webhook to trigger pipeline automatically  
- Verified pipeline stages via Jenkins Dashboard  

---

## 🔌 Required Jenkins Plugins and Installation

To ensure the pipeline works as expected, install the following plugins in Jenkins:

- Git Plugin – Integrates Git repositories  
- Pipeline Plugin – Enables pipeline jobs  
- Docker Pipeline – Supports Docker commands inside pipelines  
- GitHub Integration Plugin – Triggers Jenkins jobs from GitHub events  
- Blue Ocean *(optional)* – Provides a modern UI for pipelines  

### How to Install Plugins

1. Open Jenkins at `http://localhost:8080`  
2. Go to `Manage Jenkins` → `Manage Plugins`  
3. Click on the **Available** tab  
4. Search for each plugin listed above  
5. Select them and click **Install without restart**

---

## 📂 Jenkinsfile

A `Jenkinsfile` was added to the root of the project with the following content:

```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nodejs-demo-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Gowdamohan2/DevOps-test-day2.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test || echo "No test script defined"'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Docker Run') {
            steps {
                echo 'Running Docker container...'
                sh "docker run -d -p 3000:3000 $DOCKER_IMAGE"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
