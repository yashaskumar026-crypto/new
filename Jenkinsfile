pipeline {
    agent any

    environment {
        IMAGE_NAME = "yashas11/jenkins-html-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub1',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker stop html-container || true
                docker rm html-container || true
                docker run -d --name html-container -p 8081:80 $IMAGE_NAME
                '''
            }
        }
    }
}
