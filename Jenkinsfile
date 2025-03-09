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
        echo "Aplikasi berjalan selama 1 menit.."
        sleep(time: 1, unit: 'MINUTES')
        sh './jenkins/scripts/kill.sh'
    }
}
