node {
    stage('Build') {
        docker.image('node:16-buster-slim').inside('--user root') {
            stage('Install Dependencies') {
                sh 'apt-get update && apt-get install -y npm'
            }

            stage('Builds') {
                sh 'npm install'
            }

        }
    }

    stage('Test') {
        sh './jenkins/scripts/test.sh'
    }

    stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
    }

    stage('Deploy') {
        sh './jenkins/scripts/deliver.sh'
        sleep(time: 1, unit: 'MINUTES')
    }

}
