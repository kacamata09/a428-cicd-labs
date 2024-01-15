// node {
//     docker.image('node:16-buster-slim').withRun('-p 3000:3000') {

//         stage('Build') {
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
                // sh 'rm -r node_modules'
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
    }
}