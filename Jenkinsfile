pipeline {
    agent any

    tools {
        maven 'Maven3'  
    }

    stages {

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

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {
                    sh 'pwd'  // Check the current directory
                    sh 'ls -la'  // List files to verify the presence of pom.xml
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    sh 'pwd'  // Check the current directory
                    sh 'ls -la'  // List files to verify the presence of pom.xml
                    sh 'mvn clean install'
                }
            }
        }

    }
}
