pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'SonarQubeLocal'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kittichai/myapp.git'
            }
        }
        stage('Debug') {
            steps {
                sh 'ls -la'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh 'chmod +x ./gradlew' // ทำให้ gradlew รันได้ (Linux/Mac)
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}
