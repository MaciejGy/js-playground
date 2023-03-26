pipeline {
    agent {
        docker {
            image 'node:18'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Npm install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run test') {
            steps {
                sh 'chmod u+x ./node_modules/.bin/*'                
                sh 'npm test'
            }
        }
    }
    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}