pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls -la'  // List files to verify the directory structure
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {
                    sh 'mvn clean install'  // Run Maven in the Employee-Service directory
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    sh 'mvn clean install'  // Run Maven in the Department-Service directory
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
