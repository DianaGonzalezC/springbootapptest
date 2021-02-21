pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build_') {
            steps {
                sh './gradlew assemble'
            }
        }
        stage('Test_') {
            steps {
                sh './gradlew test'
            }
        }


        stage('Build Docker image') {
            steps {
                sh './gradlew docker'
            }
        }

        stage('Push Docker image') {
            steps {
                sh 'docker login -u AWS -p (aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 196260458954.dkr.ecr.us-east-2.amazonaws.com')
                sh 'docker tag 4759d12b20c5 196260458954.dkr.ecr.us-east-2.amazonaws.com/testspringbootapp:latest'
                sh 'docker push 196260458954.dkr.ecr.us-east-2.amazonaws.com/testspringbootapp:latest'
            }
        }

    }
}