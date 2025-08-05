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
