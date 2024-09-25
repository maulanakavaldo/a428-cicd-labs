// Scripted Pipeline

node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            // Menambahkan input untuk manual approval
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed', submitter: 'admin'
        }

        stage('Deploy') {
            // Menjalankan skrip deliver.sh untuk melakukan deploy
            sh './jenkins/scripts/deliver.sh'

            // Menunggu selama 1 menit agar aplikasi bisa digunakan
            echo "Aplikasi sudah di-deploy. Menunggu selama 1 menit..."
            sleep 60
            
            // Setelah 1 menit, jalankan skrip kill.sh untuk menghentikan aplikasi
            sh './jenkins/scripts/kill.sh'
        }
    }
}


/*
=============================
Declarative Pipeline
=============================
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
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
} 
*/
