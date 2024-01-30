// node {
//     docker.image('node:16-buster-slim').withRun('-p 3000:3000') {

//         stage('Build') {
//             sh 'npm cache clean -f'
//             // sh 'rm -r node_modules'
//             sh 'npm install'
//         }

//         stage('Test') {
//             sh './jenkins/scripts/test.sh'
//         }
   
//     }
// }

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
                sh 'npm cache clean -f'
                // sh 'npm install -g npm'
                // sh 'rm -r node_modules'
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }

        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke stage deploy? (Klik "Proceed" untuk melanjutkan)'
            }
        }

        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                timeout(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh'
            }
        }

    }
}