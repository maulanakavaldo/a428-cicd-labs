// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim'
//             args '-p 4000:4000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') { 
//             steps {
//                 sh './jenkins/scripts/test.sh' 
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
//     }
// }

node {
    // Menggunakan Docker untuk menjalankan agent
    stage('Prepare Environment') {
        // Menjalankan Docker container dengan Node.js
        docker.image('node:16-buster-slim').inside('-p 4000:4000') {
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
            stage('Deploy') {
                steps {
                    sh './jenkins/scripts/deliver.sh'
                    input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                    sh './jenkins/scripts/kill.sh'
                }
            }
        }
    }
}
