pipeline {
    agent any

    tools {
        maven 'Maven3'  
    }

    stages {

        // Check environment setup
        stage('Check Environment') {
            steps {
                sh 'echo "Checking Maven version..."'
                sh 'mvn -v'  // Shows Maven version
                sh 'java -version'  // Shows Java version
                sh 'which mvn'  // Shows the path to Maven
                sh 'echo $PATH'  // Shows the current PATH variable
                sh 'echo $SHELL'  // Shows the shell being used (bash, zsh, etc.)
                sh 'env'  // Displays all environment variables
            }
        }

        // Checkout the code
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        // Build Employee Service
        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {
                    sh 'mvn clean install'
                }
            }
        }

        // Build Department Service
        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    sh 'mvn clean install'
                }
            }
        }

    }
}
