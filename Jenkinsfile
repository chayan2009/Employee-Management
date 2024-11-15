pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls -la'  // List files to ensure repo is checked out correctly
                sh 'pwd'      // Confirm the current directory in the workspace
            }
        }

        stage('Build Services') {
            parallel {
                stage('Build Employee Service') {
                    steps {
                        dir('Employee-Service') {  // Change directory to Employee-Service
                            sh 'pwd'  // Verify we're in Employee-Service
                            sh '/Users/chayan/.jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven3/bin/mvn clean install'  // Use full path to Maven
                        }
                    }
                }
                stage('Build Department Service') {
                    steps {
                        dir('Department-Service') {  // Change directory to Department-Service
                            sh 'pwd'  // Verify we're in Department-Service
                            sh '/Users/chayan/.jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven3/bin/mvn clean install'  // Use full path to Maven
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
