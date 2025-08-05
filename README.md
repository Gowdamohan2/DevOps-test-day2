# 🚀 Jenkins CI/CD Pipeline – Task 2

This project demonstrates the creation of a simple yet effective CI/CD pipeline using **Jenkins** and **Docker** to automate the build and deployment process of a sample Node.js application.

---

## 🎯 Objective

Set up a basic Jenkins pipeline to automate the **build**, **test**, and **deploy** stages of an application using industry-standard tools and best practices.

---

## 🛠️ Tools & Technologies

- **Jenkins** – For orchestrating CI/CD workflow.
- **Docker** – Containerization of Jenkins and the application.
- **GitHub** – For source code management and webhook triggers.
- **Node.js** – Sample application for testing the pipeline.
- **localhost.run** – Used to expose Jenkins for webhook integration.

---

## ✅ What Was Done

- Set up a **local Jenkins environment** using Docker.
- Created a `Jenkinsfile` with clearly defined pipeline stages.
- Configured a **CI/CD pipeline** to automatically run on every code push.
- Integrated **GitHub webhook** to trigger Jenkins jobs on commits.
- Validated the pipeline execution through the Jenkins dashboard.

---

## 🧪 Pipeline Stages

The `Jenkinsfile` contains the following stages:

- **Build** – Installs the required dependencies.
- **Test** – (Optional) Runs unit or integration tests.
- **Deploy** – Starts the application in a Docker container.

---

## 🔁 GitHub Webhook

A webhook was configured in the GitHub repository to notify Jenkins on every push, allowing the pipeline to run automatically without manual triggers.

---

## 📂 Jenkinsfile

A declarative `Jenkinsfile` was created in the root of the project repository. This file defines the pipeline structure and includes the build, test, and deploy stages.

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add test command if available
            }
        }
        stage('Deploy') {
            steps {
                echo 'Starting the app...'
                sh 'npm start'
            }
        }
    }
}


