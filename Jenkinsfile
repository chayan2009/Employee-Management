pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
                // List files in the workspace to verify the structure
                sh 'ls -la'
            }
        }

        stage('Build Employee Service') {
            steps {
                // Build Employee Service
                dir('Employee-Service') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                // Build Department Service
                dir('Department-Service') {
                    sh 'mvn clean install'
                }
            }
        }
    }

    post {
        always {
            // Archive any built artifacts, even if no build happens
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
            // Consider sending notifications or triggering other actions on failure
        }
    }
}
