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
        stage('Create Change Request in ServiceNow') {
            steps {
                snDevOpsChange(
                    changeCreationTimeOut: 3600,
                    changeStepTimeOut: 18000,
                    pollingInterval: 60,
                    configurationName: 'Jenkins Win Server',  // nome da configuração no Jenkins
                    changeRequestDetails: '''{
                        "attributes": {
                            "short_description": "Deploy React App - Jenkins Pipeline",
                            "priority": "2",
                            "start_date": "2025-09-20 08:00:00",
                            "end_date": "2025-09-20 18:00:00",
                            "justification": "Deploy automático via Jenkins",
                            "description": "Pipeline de build React acionado via Jenkins.",
                            "cab_required": false,
                            "comments": "Change criada automaticamente via Jenkinsfile",
                            "work_notes": "Gerado no pipeline",
                            "assignment_group": "a715cd759f2002002920bde8132e7018"
                        },
                        "setCloseCode": false,
                        "autoCloseChange": true
                    }'''
                )
            }
        }
        stage('Archive build artifacts') {
            steps {
                archiveArtifacts artifacts: '.next/**', fingerprint: true
            }
        }
    }
}