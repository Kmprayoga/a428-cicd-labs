/*
node {
    stage('Prepare Environment') {
        docker.image('node:16-buster-slim').inside('--user root') {
            stage('Install Dependencies') {
                sh 'apt-get update && apt-get install -y npm'
            }

            stage('Build') {
                sh 'npm install'
            }

            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
        }
    }

    stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
    }

    stage('Deploy') {
        sh './jenkins/scripts/deliver.sh'
        sleep(time: 1, unit: 'MINUTES')
    }

}
*/
pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
        }

        stage('Deploy') {
        sh './jenkins/scripts/deliver.sh'
        sleep(time: 1, unit: 'MINUTES')
        }
    }
}