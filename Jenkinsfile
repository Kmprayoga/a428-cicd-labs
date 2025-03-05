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

            stage('Deploy'){
                sh './jenkins/scripts/deliver.sh'
                input message : "end of app"
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
