pipeline {
    agent any

    environment {
        registry = "health-status-api"
    }

    stages {
        stage("Clone Repository") {
            steps {
                checkout scm
            }
        }
        stage("Install Dependencies") {
            steps {
                sh "npm install"
            }
        }
        stage("Run Tests") {
            steps {
                sh "echo Running tests (placeholder)"
            }
        }
        stage("Build Docker Image") {
            steps {
                script {
                    // Build Docker image locally
                    dockerImage = docker.build("$registry:${env.BUILD_ID}")
                }
            }
        }
        stage("Deploy Container") {
            steps {
                // Run Docker container locally
                sh "docker run -d -p 3000:3000 $registry:${env.BUILD_ID}"
            }
        }
    }

    post {
        always {
            script {
                dockerImage.remove() // Clean up image after use
            }
        }
    }
}
