pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "springboot-app"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tonmoym83/DemoKubernetes.git'
            }
        }

        stage('Build JAR') {
            steps {
                bat 'mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% ."
            }
        }

        stage('Run on Docker Desktop') {
            steps {
                // Stop old container if running
                bat "docker rm -f springboot-container || echo 'No old container'"

                // Run new container locally
                bat "docker run -d -p 8080:8080 --name springboot-container %DOCKER_IMAGE%:%DOCKER_TAG%"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Apply manifests to Docker Desktop’s built-in Kubernetes
                bat "kubectl apply -f k8s\\deployment.yaml"
                bat "kubectl apply -f k8s\\service.yaml"
            }
        }
    }
}
