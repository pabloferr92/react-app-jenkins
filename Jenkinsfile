pipeline {
    agent any

    tools {
        nodejs "node" // nome configurado no Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/pabloferr92/react-app-jenkins.git',
                    credentialsId: '5aeac2b9-cc45-4ca0-a4a1-83076370436f'
            }
        }
        stage('Install dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }
        stage('Archive build artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}