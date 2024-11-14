pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/dudun124/a428-cicd-labs', branch: 'master'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
    }
}
