pipeline {
    agent any

    environment {
        // ใช้ Jenkins Credentials ID แบบ Secret Text หรือ Username/Password
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
        DOCKER_IMAGE = "https://hub.docker.com/repository/docker/keng2docker/jenkin_hub"   // เปลี่ยนเป็น Docker Hub จริงของคุณ
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                  git url: 'https://github.com/kittichai/myapp.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }

        stage('Login & Push to Docker Hub') {
            steps {
                script {
                    sh """
                        echo "$DOCKERHUB_CREDENTIALS_PSW" | docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin
                        docker push $DOCKER_IMAGE:$DOCKER_TAG
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build and Push Success!"
        }
        failure {
            echo "❌ Build or Push Failed."
        }
    }
}
