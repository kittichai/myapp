pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'SonarQubeLocal'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main','https://github.com/kittichai/myapp.git' main
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
