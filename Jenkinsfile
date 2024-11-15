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
                sh 'mvn clean install -f Employee-Service/pom.xml'  // Run Maven build for Employee Service
            }
        }

        stage('Build Department Service') {
            steps {
                sh 'mvn clean install -f Department-Service/pom.xml'  // Run Maven build for Department Service
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
