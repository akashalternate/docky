pipeline {
    agent any

    environment {
        IMAGE_NAME = 'docky-app'
        CONTAINER_NAME = 'docky-container'
        PORT = '8080'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/akashalternate/docky.git', branch: 'main'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo '✅ Docker container deployed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
