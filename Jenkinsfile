pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/fadhil19/P8_Jenkins_Test'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'npm run test:unit'
            }
        }
        stage('Run Integration Tests') { // Stage baru untuk integration tests
            steps {
                bat 'npm run test:integration' // Perintah untuk menjalankan integration tests
            }
            post {
                success {
                    emailext subject: 'Integration Tests Succeeded', body: 'The Integration Tests stage succeeded!', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
                failure {
                    emailext subject: 'Integration Tests Failed', body: 'The Integration Tests stage failed.', 
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Tambahkan perintah build jika diperlukan
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Tambahkan perintah deploy jika diperlukan
            }
        }
    }
    post {
        success {
            echo 'Pipeline finished successfully!'
            emailext subject: 'Pipeline Succeeded', body: 'The pipeline finished successfully!', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
        failure {
            echo 'Pipeline failed!'
            emailext subject: 'Pipeline Failed', body: 'The pipeline failed.', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
    }
}
