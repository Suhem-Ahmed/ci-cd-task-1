pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "suhemahmed/nodejs-demo-app:${env.BUILD_ID}"
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub')
    }

    stages {
        // Checkout code from GitHub
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Suhem-Ahmed/ci-cd-task-1.git'
            }
        }

        // Install dependencies and run tests
        stage('Build & Test') {
            steps {
                sh 'npm install'
                sh 'npm test'  // Ensure your package.json has a "test" script
            }
        }

        // Build Docker image (using Docker-in-Docker)
        stage('Docker Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        // Push to Docker Hub
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        // Deploy (example: run container locally inside Jenkins)
        stage('Deploy') {
            steps {
                sh "docker run -d -p 3000:3000 ${DOCKER_IMAGE}"
            }
        }
    }

    // Clean up
    post {
        always {
            sh 'docker rmi -f $(docker images -q) || true'
        }
    }
}
