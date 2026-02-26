pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t projeto-devops .'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker rm -f projeto-devops-container || exit 0
                docker run -d -p 8095:80 --name projeto-devops-container projeto-devops
                '''
            }
        }

        stage('Smoke Test') {
            steps {
                bat 'curl http://localhost:8095'
            }
        }
    }

    post {
        always {
            bat 'docker rm -f projeto-devops-container || exit 0'
        }
    }
}