pipeline {
    agent any

    tools {
        // Use the Maven tool installed in Jenkins (adjust the name to match your installation)
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Employee Service') {
            steps {
                dir('Employee-Service') {
                    // Use Maven to build the Employee-Service
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    // Use Maven to build the Department-Service
                    sh 'mvn clean install'
                }
            }
        }
    }
}
