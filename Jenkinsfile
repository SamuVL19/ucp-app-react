pipeline {
    agent any
    tools {
        nodejs 'Node_24'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SamuVL19/ucp-app-react.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'npm test -- --watchAll=false --silent > test-output.txt'
                sh 'cat test-output.txt'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'test-output.txt', allowEmptyArchive: true
        }
        success {
            echo 'Pipeline ejecutado con éxito!'
        }
        failure {
            echo 'Pipeline fallido. Revisar logs.'
        }
    }
}
