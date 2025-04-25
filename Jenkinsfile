pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'SonarQubeLocal'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kittichai/myapp.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}
