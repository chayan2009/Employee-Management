pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Debug Workspace') {
            steps {
                sh 'ls -R'  // List all files in the workspace
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('employee-service') {
                    sh './mvnw clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('department-service') {
                    sh './mvnw clean install'
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
