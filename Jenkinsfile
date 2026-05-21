pipeline {
    agent {label 'devops1-peserta7'}    
    tools {nodejs "nodejs 18.16.0"}

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/panduaksoro/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar \
                -Dsonar.host.url=http://172.23.7.217:9000 \
                -Dsonar.token=sqp_d55ea000920cf2bb339e504efa1ca137a7de10f2 \
                -Dsonar.projectKey=simple-apps'''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}