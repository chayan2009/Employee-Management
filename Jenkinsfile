pipeline {
    agent any

    tools {
        maven 'Maven3' // Ensure Maven3 is installed and configured in Jenkins
    }

    environment {
        GIT_REPO = 'https://github.com/chayan2009/Employee-Management.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                checkout([$class: 'GitSCM',
                    branches: [[name: "*/${BRANCH}"]],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'CleanCheckout']],
                    userRemoteConfigs: [[url: GIT_REPO]]
                ])
            }
        }

        stage('Build Services') {
            steps {
                script {
                    // Navigate to Employee-Service and build
                    if (fileExists('Employee-Service/pom.xml')) {
                        dir('Employee-Service') {
                            echo "Building Employee-Service..."
                            sh './mvnw clean install' // Use Maven wrapper or replace with `mvn` if not used
                        }
                    } else {
                        error "Employee-Service pom.xml not found!"
                    }

                    // Navigate to Department-Service and build
                    if (fileExists('Department-Service/pom.xml')) {
                        dir('Department-Service') {
                            echo "Building Department-Service..."
                            sh './mvnw clean install' // Use Maven wrapper or replace with `mvn` if not used
                        }
                    } else {
                        error "Department-Service pom.xml not found!"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Build completed successfully!"
            mail to: 'vikasbk0777@gmail.com, chayanchowdhury@gmail.com',
                 subject: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build succeeded!\n\nCheck details here: ${env.BUILD_URL}"
        }

        failure {
            echo "Build failed!"
            mail to: 'vikasbk0777@gmail.com, chayanchowdhury@gmail.com',
                 subject: "Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed.\n\nCheck details here: ${env.BUILD_URL}"
        }
    }
}
