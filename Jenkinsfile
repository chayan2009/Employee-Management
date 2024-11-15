pipeline {
    agent {
        docker {
            image 'maven:3.8.4-jdk-11'  // Use Maven Docker image
            args '-v /tmp:/tmp'  // Optional: Volume mount for temp files
        }
    }
    stages {
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
