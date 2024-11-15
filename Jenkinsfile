pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls -la'
            }
        }

        stage('Build Services') {
            parallel {
                stage('Build Employee Service') {
                    steps {
                        dir('Employee-Service') {
                            sh 'mvn clean install'
                        }
                    }
                }
                stage('Build Department Service') {
                    steps {
                        dir('Department-Service') {
                            sh 'mvn clean install'
                        }
                    }
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
            // Consider sending notifications or triggering other actions on failure
        }
    }
}