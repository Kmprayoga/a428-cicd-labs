node {
    stage('Build') {
        docker.image('node:16-buster-slim').inside('--user root') {
            stage('Install Dependencies') {
                sh 'npm install'
            }

            stage('Builds') {
                sh 'npm run build'
            }
        }
    }

    stage('Test') {
        docker.image('node:16-buster-slim').inside('--user root') {  
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
