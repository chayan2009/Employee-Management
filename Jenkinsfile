pipeline {
    agent any

    tools {
        maven 'Maven3' // Ensure Maven is configured in Jenkins
    }

    environment {
        GIT_REPO = 'https://github.com/chayan2009/Employee-Management.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clean workspace and checkout the repository
                    checkout([$class: 'GitSCM',
                        branches: [[name: "*/${BRANCH}"]],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'CleanCheckout']],
                        userRemoteConfigs: [[url: GIT_REPO]]
                    ])
                }
                // Debugging: Verify the workspace structure
                sh 'ls -la'
            }
        }

        stage('Debug Workspace') {
            steps {
                echo "Debugging workspace structure..."
                sh '''
                echo "Current directory: $(pwd)"
                echo "Workspace structure:"
                ls -la
                echo "Contents of Employee-Service:"
                ls -la Employee-Service || echo "Employee-Service directory missing"
                echo "Contents of Department-Service:"
                ls -la Department-Service || echo "Department-Service directory missing"
                '''
            }
        }

        stage('Build Services') {
            steps {
                script {
                    // Build Employee-Service
                    if (fileExists('Employee-Service/pom.xml')) {
                        echo "Building Employee-Service..."
                        dir('Employee-Service') {
                            sh './mvnw clean install'
                        }
                    } else {
                        echo "Employee-Service directory or POM file missing!"
                    }

                    // Build Department-Service
                    if (fileExists('Department-Service/pom.xml')) {
                        echo "Building Department-Service..."
                        dir('Department-Service') {
                            sh './mvnw clean install'
                        }
                    } else {
                        echo "Department-Service directory or POM file missing!"
                    }
                }
            }
        }

        stage('Post-Build Cleanup') {
            steps {
                echo "Cleaning up workspace..."
                cleanWs()
            }
        }
    }

    post {
        success {
            echo "Build completed successfully!"
        }
        failure {
            echo "Build failed. Please check the logs."
        }
        always {
            echo "Pipeline execution finished."
        }
    }
}
