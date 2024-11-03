pipeline {
    agent any

    environment {
        registry = "abhisheksamuel/health-status-api" // Replace with your Docker Hub username
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
                    // Build Docker image
                    dockerImage = docker.build("$registry:${env.BUILD_ID}")
                }
            }
        }
        stage("Push Docker Image") {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    docker.withRegistry("https://registry.hub.docker.com", "dockerhub-credentials") {
                        dockerImage.push()
                    }
                }
            }
        }
        stage("Deploy Container") {
            steps {
                // Run Docker container
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
