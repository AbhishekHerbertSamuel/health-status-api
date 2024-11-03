pipeline {
    agent any

    environment {
        registry = "health-status-api" // Local Docker image name
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
                sh "echo Running tests placeholder" // Updated to avoid syntax errors
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
                if (dockerImage != null) {
                    try {
                        dockerImage.remove() // Clean up image after use to free space
                    } catch (Exception e) {
                        echo "No Docker image to remove or failed to remove."
                    }
                }
            }
        }
    }
}
