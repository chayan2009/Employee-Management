pipeline {
    agent any

    tools {
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
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                    sh 'mvn clean install'
                }
            }
        }
    }
}
