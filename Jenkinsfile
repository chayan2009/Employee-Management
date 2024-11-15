pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout the repository
            }
        }

        stage('Debug Workspace') {
            steps {
                sh 'ls -R'  // List all files in the workspace to verify the structure
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {  // Navigate to the employee-service directory
                    sh 'mvn clean install -f pom.xml'  // Run Maven build inside this directory
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {  // Navigate to the department-service directory
                    sh 'mvn clean install -f pom.xml'  // Run Maven build inside this directory
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
