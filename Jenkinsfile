pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout the repository
                sh 'ls -R'     // List all files to verify the structure after checkout
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {  // Navigate to Employee-Service directory
                    sh 'mvn clean install'  // Run Maven build for Employee Service
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {  // Navigate to Department-Service directory
                    sh 'mvn clean install'  // Run Maven build for Department Service
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true  // Archive the build artifacts (JAR files)
        }
        success {
            echo 'Pipeline succeeded!'  // Success message if the build passes
        }
        failure {
            echo 'Pipeline failed!'  // Failure message if the build fails
        }
    }
}
