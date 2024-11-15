pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout the repository
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('employee-service') {  // Navigate to the employee-service directory
                    sh './mvnw clean install'  // Run Maven build inside this directory
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('department-service') {  // Navigate to the department-service directory
                    sh './mvnw clean install'  // Run Maven build inside this directory
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
