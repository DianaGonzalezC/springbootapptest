pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }stage('Build Docker image') {
            steps {
                sh './gradlew build docker dockerRun'
            }
        }stage('Push Docker image') {
            steps {
                sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 196260458954.dkr.ecr.us-east-2.amazonaws.com'
                sh 'docker tag 4759d12b20c5 196260458954.dkr.ecr.us-east-2.amazonaws.com/testspringbootapp:latest'
                sh 'docker push 196260458954.dkr.ecr.us-east-2.amazonaws.com/testspringbootapp:latest'
            }
        }
    }
}