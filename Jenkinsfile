pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls -la'  // List the files to ensure the repo is checked out correctly
            }
        }

        stage('Build Services') {
            parallel {
                stage('Build Employee Service') {
                    steps {
                        dir('Employee-Service') {  // Move into the Employee-Service directory
                            sh '/Users/chayan/.jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven3/bin/mvn clean install'  // Use the full path to Maven
                        }
                    }
                }
                stage('Build Department Service') {
                    steps {
                        dir('Department-Service') {  // Move into the Department-Service directory
                            sh '/Users/chayan/.jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven3/bin/mvn clean install'  // Use the full path to Maven
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
        }
    }
}
