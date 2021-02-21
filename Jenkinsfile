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


    }
}