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
        stage('export modules') {
            steps {
                zip zipFile: 'modules.zip', archive: false, dir: 'archive'
                archiveArtifacts artifacts: 'modules.zip', fingerprint: true
            }
        }
        stage('import modules & Run test') {
            steps {
                copyArtifacts filter: 'modules.zip', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER)
                unzip zipFile: 'modules.zip', dir: './archive_new'
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