pipeline {
    agent any



        stage('Build') {
            steps {
                echo 'Building HTML project...'

                sh '''
                test -f index.html
                test -f style.css
                test -f script.js
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh '''
                sudo cp -r * /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
