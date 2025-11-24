pipeline {
    agent any

  tools {
        maven 'Maven3'   // matches the name in Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tonmoym83/DemoKubernetes.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

 stage('Docker Build') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Deploy to Docker Desktop') {
            steps {
                // Stop old container if running
                bat "docker rm -f springboot-container || echo No old container"

                // Run new container
                bat "docker run -d -p 8080:8080 --name springboot-container %DOCKER_IMAGE%:%DOCKER_TAG%"
            }
        }
    }

}
