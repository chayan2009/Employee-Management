pipeline {
    agent any
    tools {
        maven 'Maven3'  // Ensure Maven is configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Services') {
            steps {
                script {
                    // Build Employee-Service
                    dir('Employee-Service') {
                        echo "Building Employee-Service..."
                        sh 'mvn clean install'
                    }
                    // Build Department-Service
                    dir('Department-Service') {
                        echo "Building Department-Service..."
                        sh 'mvn clean install'
                    }
                }
            }
        }
    }
}
