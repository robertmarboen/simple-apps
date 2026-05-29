pipeline {

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/robertmarboen/simple-apps.git'
            }
        }

        stage('Build') {
            steps {
               sh '''cd app
               npm install'''
            }
        }

        stage('Testing App') {
            steps {
               sh '''cd app
               npm test
               npm test:coverage'''
            }
        }

        stage('Code Analys') {
            steps {
               sh '''sonar-scanner \
                        -Dsonar.projectKey=simple-apps \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://172.23.8.73:9000 \
                        -Dsonar.token=sqp_4ddc177f49fa5ce136b0c6c15b76e1156c6b039d'''
            }
        }

        stage('Deploy App') {
            steps {
               sh '''
               docker compose build
               docker compose up -d'''
            }
        }
    }
}
