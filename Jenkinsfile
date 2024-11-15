pipeline {
    agent any

    tools {
        maven 'Maven3'  // Use the Maven tool installed in Jenkins
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
                    // Run Maven build in Employee-Service directory
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    // Run Maven build in Department-Service directory
                    sh 'mvn clean install'
                }
            }
        }
    }
}
