pipeline {
    agent any

    environment {
        IMAGE_NAME = 'docky-app'
        CONTAINER_NAME = 'docky-container'
        PORT = '8050'
    }

    stages {

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
            echo '✅ Success!'
        }
        failure {
            echo '❌ Failed!'
        }
    }
}
