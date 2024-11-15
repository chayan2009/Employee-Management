pipeline {
    agent any

    environment {
        // Set any environment variables if needed
        // E.g., MAVEN_HOME, JAVA_HOME, etc.
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from Git
                checkout scm
            }
        }
        stage('Build Employee Service') {
            steps {
                dir('employee-service') { // Navigate to employee service directory
                    script {
                        // If using Maven wrapper (./mvnw)
                        sh './mvnw clean install'
                        // Or if using global Maven installation
                        // sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Build Department Service') {
            steps {
                dir('department-service') { // Navigate to department service directory
                    script {
                        // If using Maven wrapper (./mvnw)
                        sh './mvnw clean install'
                        // Or if using global Maven installation
                        // sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Run Tests') {
            steps {
                // You can add unit tests or integration tests if required
                echo 'Running tests...'
            }
        }
        stage('Deploy Services') {
            steps {
                // Add deployment steps if applicable (e.g., Docker, Kubernetes, etc.)
                echo 'Deploying services...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            // Clean up or archive artifacts if necessary
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
