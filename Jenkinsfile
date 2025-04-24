pipeline {
    agent any
    environment {
        // กำหนดตัวแปรสำหรับ Docker Hub credentials
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        // ชื่อ Docker image
        IMAGE_NAME = "myapp:${env.BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                // ดึงโค้ดจาก GitHub
                git branch: 'main', url: 'https://github.com/kittichai/myapp.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image จาก Dockerfile
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Test') {
            steps {
                // รัน container เพื่อทดสอบ (ตัวอย่าง)
                sh 'docker run --rm ${IMAGE_NAME} npm test'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // ล็อกอินและ push image ไป Docker Hub
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker tag ${IMAGE_NAME} your-dockerhub-username/${IMAGE_NAME}'
                sh 'docker push your-dockerhub-username/${IMAGE_NAME}'
            }
        }
        stage('Cleanup') {
            steps {
                // ลบ image ในเครื่องเพื่อประหยัดพื้นที่
                sh 'docker rmi ${IMAGE_NAME}'
            }
        }
    }
    post {
        always {
            // ล้าง workspace
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
