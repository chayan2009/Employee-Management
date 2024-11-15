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
                    sh '/path/to/maven/bin/mvn -f Employee-Service/pom.xml clean install'
                }
            }
        }
        stage('Build Department Service') {
            steps {
                dir('Department-Service') {
                     sh '/path/to/maven/bin/mvn -f Employee-Service/pom.xml clean install'
                }
            }
        }
    }
}
