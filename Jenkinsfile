pipeline {
    agent { label 'agent' }

    environment {
        IMAGE_NAME = "jenkins-docker-demo"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Code GitHub se checkout ho raha hai...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Docker image build ho rahi hai...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage abhi placeholder hai - yahan automation tests chalenge'
                sh 'docker images | grep $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Purana container hatao, naya deploy karo...'
                sh '''
                    docker stop $IMAGE_NAME || true
                    docker rm $IMAGE_NAME || true
                    docker run -d --name $IMAGE_NAME -p 8081:80 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline successfully complete ho gaya!'
        }
        failure {
            echo '❌ Pipeline fail ho gaya, logs check karo.'
        }
    }
}
